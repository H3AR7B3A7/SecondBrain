## Npm
Npm is a package manager for [[JavaScript]] projects. It is the default package manager for [[Angular]].

Npm keeps track of the specific dependencies of different packages in package-lock.json.
In older versions we had to use:

> npm shrinkwrap

We also had to use --save to add them to package.json:

> npm install packageName --save

Luckily we no longer have to do either of these things. These are some of the things npm package manager learned from some of the alternatives.

## Yarn
Yarn is an alternative package manager that has some advantages over npm:

- Yarn caches every package it downloads so it never needs to download it again. It also parallelizes operations to maximize resource utilization so install times are faster than ever.
- Yarn uses checksums to verify the integrity of every installed package before its code is executed.
- Using a detailed, but concise, lockfile format, and a deterministic algorithm for installs, Yarn is able to guarantee that an install that worked on one system will work exactly the same way on any other system.

To change our package manager globally we use:

> ng config -g cli.packageManager yarn

To add packages we use:

> yarn add packageName

To find out why a package exists on your project:

> yarn why packageName



---
#GoodPractice