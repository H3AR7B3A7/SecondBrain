# Feign

[GitHub Repo](https://github.com/OpenFeign/feign)

Feign is a [[Java]] to HTTP client binder inspired by Retrofit, JAXRS-2.0, and WebSocket. Feign's first goal was reducing the complexity of binding Denominator uniformly to HTTP APIs regardless of ReSTfulness.

Feign works by processing annotations into a templated request. Arguments are applied to these templates in a straightforward fashion before output. Although Feign is limited to supporting text-based APIs, it dramatically simplifies system aspects such as replaying requests. Furthermore, Feign makes it easy to unit test your conversions knowing this.

It is much cleaner than using a RestTemplate, because it separates business logic from the client code, making it more readable and reusable.



---
#Java #Library