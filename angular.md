Angular
=======

* https://angular.io/


Installation
------------

```
$ npm install -g @angular/cli
```

만약 설치 시 오류가 발생할 경우에는 다음과 같이 삭제 하고 다시 설치한다.
```
npm uninstall -g @angular/cli
npm cache verify
# if npm version is < 5 then use `npm cache clean`
npm install -g @angular/cli@latest
```

Getting Started
---------------

Start a new logic project using `ng new`:

```
$ ng new giphy-app
```

Run your App
------------

Run your app in the browser (great for initial development):
```
$ cd giphy-app
$ ng serve 
```

Navigate to http://localhost:4200/. 

TIP: The app will automatically reload if you change any of the source files.

Reference
---------

* https://cli.angular.io/