# Gulp Tutorial as I have learned from Alecaddd (Alessandro Castellani)
Youtube Channel: https://www.youtube.com/channel/UCbmBY_XYZqCa2G0XmFA7ZWg

# Development Environment using NodeJS and Gulp


1.   Download latest 64-bit version of NodeJS from https://nodejs.org/en/.
     Install it. This will install NodeJS and NPM (NodeJS Package Manager).

2.   NPM comes with it's own command prompt, called, "Node.js command prompt. Click and open it.

3.   Install GulpJS globally from NPM. Type

```
npm install --save-dev gulp
```

and press Enter key.

# Create package.json file

1.   Type

```
npm init
```

and press enter.

2.   NPM will start asking you about your project one by one. Respond to the questions by typing in your correct inputs.
     At the end, a **"package.json"** file will be created for me.
     Beside this, a **package-lock.json** is also created. This file keeps a log of what I do with Gulp.

3.   If necessary. open the "**package.json**" file and inspect it if you need any modification in it.
4.   Now, type the following command

```
npm install --save-dev gulp
```

NPM will install all dependencies from the NPM repository for your project.

If any developer ever need the exact package.json file for his project, send it to him.
The developer just need to issue the command:

```
npm install
```

NPM will recognize that your already have a package.json file and download all files dependent for your project.

# To import a Dev Dependency in your project

```
npm install --save-dev gulp-rename
or,
npm install --save-dev gulp-sass
or,
npm install --save-dev less-plugin-autoprefix
```    

এখন প্রোজেক্টের রুট ডিরেক্টরিতে gulpfile.js নামে একটি ফাইল ক্রিয়েট করতে হবে যেটাতেই মূলত Gulp এর অটোম্যাট টাস্ক রানারের কোডগুলো থাকবে। অনেকটা Config ফাইলের মতোই।

```
touch gulpfile.js
```

এবার আপনার gulpfile.js ফাইলটি আপনার পছন্দের কোড এডিটরে ওপেন করুন।

Gulp এ মূলত নিচের এই মেথডগুলোই বেশী ইউজ করা হয়। সবকিছু অনেকটা এগুলোর উপরেই করা হয়।

- **gulp.task** টাস্ক বানানোর জন্যে ইউজ করা হয়।
- **gulp.src** যে ফাইলের উপর অ্যাকশন নেওয়া হবে সেটার লোকেশান…
- **gulp.dest** অ্যাকশন নেওয়া ফাইলটা যেখানে সেইভ করবেন…
- **gulp.watch** কোনো ফাইলকে নজরদারীতে রাখার জন্যে, ঐ ফাইলে কিছু চ্যাঞ্জ হলেই আপনার দেওয়া টাস্ক অটোম্যাটিকভাবেই অ্যাপ্লাই হয়ে যাবে।

## টাস্ক তৈরী করাঃ

gulp.task দিয়ে টাস্ক ক্রিয়েট করা হয়। এটা সাধারণত দুইটা আর্গুমেন্ট নেয়। প্রথমটা আপনার টাস্কের নাম এবং দ্বিতীয়টায় একটা কলব্যাক ফাংশন। এই ফাংশনের ভিতরেই আপনি কি করতে চাচ্ছেন সেগুলোর কোড লিখবেন।

```
gulp.task('taskName', function() {
  // What do you want to do
});
```

আমরা যেহেতু gulp ইউজ করেছি তাই এটা অবশ্যই require করিয়ে নিতে হবেঃ

```
const gulp = require('gulp');
```

যেমন খুব সিম্পলভাবে একটা টেক্সট console.log করাতে চাইলেঃ
```
gulp.task('hello', function() {
   console.log('Hi! This is my First Task!!');
});
```
এখন Gulp এর এই টাস্ক রান করাতে আপনাকে gulp-cli ইউজ করতে হবে। যেহেতু আমরা এটা গ্লোবাললি ইন্সটল করে নিয়েছি তাই এখন আমরা কমান্ড লাইনে gulp কমান্ড ইউজ করতে পারবো। প্রথমে কমান্ড লাইনে gulp লিখে তারপর আপনার টাস্কের নাম লিখতে হবে। অবশ্যই মনে রাখবেন এই কমান্ড প্রোজেক্টের রুটে বা যেখানে gulpfile.js ফাইলটা রয়েছে সেখান থেকে রান করাতে হবে। এবার আমরা উপরের ডিমো console.log টা রান করাবো। আপনার কমান্ড লাইনে লিখুনঃ
```
gulp hello
```
তারপর এন্টার চাপলে দেখবেন আপনার লেখা প্রিন্ট হয়েছেঃ

![First Hello Message](https://github.com/manzurahmed/gulp-from-alecaddd/blob/master/images/hello.png)

# Default gulp task

যে কোন টাক্স রান করার জন্য আমি gulp এর পরে স্পেসিফিক ঐ টাক্স এর নাম লিখে এন্টার কি চাপ দিলেই টাক্সটি রান করবে। যেমনঃ

```
gulp style
or,
gulp js
```

এভাবে যতগুলো টাক্স আছে প্রয়োজন মত আমার টাক্সগুলোকে রান করাতে পারব। কিন্তু, বারংবার ম্যানুয়ালি টাক্স রান করা বিরক্তিকর ও কষ্টসাধ্য কাজ।

এই সমস্যার সমাধানে রয়েছে gulp এর default task রান করবার ব্যবস্থা। এ জন্য gulpfile.js ফাইলে নতুন একটি gulp.task তৈরী করব, যার নাম হবে 'default'।

```
gulp.task( 'default', ['style', 'js'];
```

এই টাক্স এ ২টা প্যারামিটারঃ টাক্সের নাম এবং যে টাক্সগুলো রান করাব তার একটি স্ট্রিং এ্যারে।

এবার, টার্মিনালে গিয়ে শুধুমাত্র gulp লিখে এন্টার কি চাপ দিলেই default টাক্সটির সাথে জুড়ে দেয়া টাক্স ২টা, 'style' এবং 'js' রান হয়ে যাবে।

```
gulp
```

# watch - It's like Magic



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
