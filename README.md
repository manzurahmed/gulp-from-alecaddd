# Gulp Tutorial as I have learned from Alecaddd (Alessandro Castellani)
Youtube Channel: https://www.youtube.com/channel/UCbmBY_XYZqCa2G0XmFA7ZWg

# Development Environment using NodeJS and Gulp


1.   Download latest 64-bit version of NodeJS from https://nodejs.org/en/.
     Install it. This will install NodeJS and NPM (NodeJS Package Manager).

2.   NPM comes with it's own command prompt, called, "Node.js command prompt. Click and open it.

3.   Install GulpJS globally from NPM. Type

```
     $ npm install --save-dev gulp
```

and press Enter key.

# Create package.json file

1.   Type

```
$ npm init
```

and press enter.

2.   NPM will start asking you about your project one by one. Respond to the questions by typing in your correct inputs.
     At the end, a **"package.json"** file will be created for me.

3.   If necessary. open the "**package.json**" file and inspect it if you need any modification in it.
4.   Now, type the following command

```
     npm install --save-dev gulp
```

NPM will install all dependencies from the NPM repository for your project.

If any developer ever need the exact package.json file for his project, send it to him.
The developer just need to issue the command:

```
    $ npm install
```

NPM will recognize that your already have a package.json file and download all files dependent for your project.

# To import a Dev Dependency in your project

```
    $ npm install --save-dev gulp-rename
or,
    $ npm install --save-dev gulp-sass
```    

# Further reading

Bangla Tutorial: https://medium.com/%E0%A6%AA%E0%A7%8D%E0%A6%B0%E0%A7%8B%E0%A6%97%E0%A7%8D%E0%A6%B0%E0%A6%BE%E0%A6%AE%E0%A6%BF%E0%A6%82-%E0%A6%AA%E0%A6%BE%E0%A6%A4%E0%A6%BE/%E0%A6%8F%E0%A6%95-%E0%A6%AA%E0%A6%B2%E0%A6%95%E0%A7%87-gulp-js-%E0%A6%9F%E0%A6%BE%E0%A6%B8%E0%A7%8D%E0%A6%95-%E0%A6%B8%E0%A7%8D%E0%A6%AC%E0%A6%AF%E0%A6%BC%E0%A6%82%E0%A6%95%E0%A7%8D%E0%A6%B0%E0%A6%BF%E0%A6%AF%E0%A6%BC-%E0%A6%95%E0%A6%B0%E0%A7%81%E0%A6%A8-f1412077b462

### ADDITIONAL READING
-----------------------

- NPM Crash Course https://www.youtube.com/watch?v=jHDhaSSKmB0
- JSON Crash Course https://www.youtube.com/watch?v=wI1CWzNtE-M
- Node.js Tutorial for Beginners https://www.youtube.com/watch?v=U8XF6AFGqlc
- Sass Workflow & Dev Server from scratch using Gulp https://www.youtube.com/watch?v=rmXVmfx3rNo
- Gulp workflow 2017 https://www.youtube.com/watch?v=KZ6LuPadEvk
- Gulp - The Basics https://www.youtube.com/watch?v=dwSLFai8ovQ

Design + Code - Hour 4.1: Project Setup (using Gulp) https://www.youtube.com/watch?v=nY4kQssg3lw

### Bootstrap 4 Crash Course https://www.youtube.com/watch?v=hnCmSXCZEpU

1. Install Gulp Globally

```
npm install -g gulp
```

2. Also install Gulp locally (development dependency)

```
npm install --save-dev gulp
```
