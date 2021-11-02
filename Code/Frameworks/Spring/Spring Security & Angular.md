# Spring Security & Angular
A simple angular application with resources secured by Spring Security.

## Http Basic 
### Spring Security Configuration
- We overwrite the default http security to only use HTTP Basic authentication.
- We change the authentication entry point to prevent the browser from prompting for credentials.
- We authorize the user to access the pages they don't need authentication for.
- We also change the csrf token repository to use a cookie instead of a header.
- We move our js, css and assets to their own directory, and make web security ignore them.
- We provide an endpoint to get the Principal.

```java
@Configuration
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .httpBasic()
                .authenticationEntryPoint((request, response, authException) 
                        -> response.sendError(HttpStatus.UNAUTHORIZED.value(), HttpStatus.UNAUTHORIZED.getReasonPhrase()))
            .and()
            .authorizeRequests()
                .antMatchers("/index.html", "/", "/home", "/login").permitAll()
                .anyRequest().authenticated()
            .and()
            .csrf()
                .csrfTokenRepository(CookieCsrfTokenRepository.withHttpOnlyFalse());
    }

    @Override
    public void configure(WebSecurity web) throws Exception {
        web.ignoring().antMatchers("/js/**", "/css/**", "/assets/images/**");
    }
}
```

### Angular Authentication & Interceptor
- We create an authentication service to send a request to the endpoint we provided with Spring,
containing an authorization header with 'Basic username:password' in base64 as value using the btoa() method.
If we get back a 200 OK, the user is authenticated, and we flip a boolean value.
- We provide an interceptor to add additional headers.

- Authentication Service:
```typescript
@Injectable({
  providedIn: 'root'
})
export class AuthenticationService {
  authenticated = false

  constructor(
    private http: HttpClient
  ) { }

  authenticate(credentials: any, callback: any) {
    const headers = new HttpHeaders(credentials ? {
      authorization: 'Basic ' + btoa(credentials.username + ':' + credentials.password)
    } : {})

    this.http.get<any>('user', { headers: headers }).subscribe(response => {
      if (response['name']) {
        this.authenticated = true
      } else {
        this.authenticated = false
      }
      return callback && callback()
    })
  }
}
```

Interceptor:
```typescript
@Injectable({
  providedIn: 'root'
})
export class XhrInterceptorService implements HttpInterceptor {

  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    const xhr = req.clone({
      headers: req.headers.set('X-Requested-With', 'XMLHttpRequest')
    });
    return next.handle(xhr);
  }
}
```

## Form Login
With a form login, we are able to add more information to the FormData than just username and password.
FormData is sent in the body of a POST request, instead of the header.

### Spring Security Configuration
```java
@Configuration
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .csrf()
                .csrfTokenRepository(CookieCsrfTokenRepository.withHttpOnlyFalse())
            .and()
            .authorizeRequests()
                .mvcMatchers(HttpMethod.GET,"/index.html", "/", "/home", "/login").permitAll()
                .anyRequest().authenticated()
            .and()
            .formLogin()
                .loginPage("/login")
                .loginProcessingUrl("/auth")
                .usernameParameter("username")
                .passwordParameter("password")
                .successHandler(successHandler())
                .failureHandler(failureHandler())
            .and()
            .logout()
                .logoutUrl("/logout")
                .logoutSuccessUrl("/");
    }

    @Override
    public void configure(WebSecurity web) throws Exception {
        web.ignoring().antMatchers("/js/**", "/css/**", "/assets/images/**");
    }

    private AuthenticationSuccessHandler successHandler() {
        return (httpServletRequest, httpServletResponse, authentication) -> {
            httpServletResponse.getWriter().append("OK");
            httpServletResponse.setStatus(200);
        };
    }

    private AuthenticationFailureHandler failureHandler() {
        return (httpServletRequest, httpServletResponse, e) -> {
            httpServletResponse.getWriter().append("Authentication failure");
            httpServletResponse.setStatus(401);
        };
    }
}
```

### Angular Authentication
```typescript
@Injectable({
  providedIn: 'root'
})
export class AuthenticationService {
  authenticated = false

  constructor(
    private http: HttpClient,
    private router: Router
  ) { }

  authenticate(credentials: any) {
    var formData: FormData = new FormData()
    formData.append('username', credentials.username)
    formData.append('password', credentials.password)

    this.http.post('auth', formData, { responseType: "text" }).subscribe(
      () => {
        this.authenticated = true
        this.router.navigateByUrl('/')
      },
      () => {
        this.authenticated = false
      }
    )
  }

  checkAuthenticationStatus() {
    this.http.get<any>('user').subscribe(response => {
      console.log('Checking: ' + response)
      if (response['name']) {
        this.authenticated = true
      } else {
        this.authenticated = false
      }
    })
  }

  logout() {
    this.http.post('logout', {}).pipe(
      finalize(() => {
        this.authenticated = false;
        this.router.navigateByUrl('/');
      })).subscribe();
  }
}
```