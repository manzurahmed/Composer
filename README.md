## Composer কি?

PHP এর ডিপেন্ডেন্সি ম্যানেজমেন্টের জন্য Composer ব্যবহার করা হয়। Composer এর মাধ্যমে আমি আমার প্রজেক্ট কোন কোন লাইব্রেরীসমূহের উপরে নির্ভরশীল তা উল্লেখ করে দিতে পারি এবং Composer আমাকে একটি autoloader তৈরী করে দিবে যার মাধ্যমে প্রজেক্টের যেখানে যেখানে প্রয়োজন সেখানে এই autoloader এর মাধ্যমে আমার প্রয়োজনীয় লাইব্রেরী ফাইলগুলো লোড করে নিতে পারব।

### Composer ইন্সটল করার নিয়ম

Ubuntu তে যে প্রোজেক্ট ফোল্ডার Composer ইন্সটল করব, সেখানে থাকা অবস্থায় নিচের কমান্ডগুলো রান করতে হবে। আমার ল্যাপটপে Xampp (lampp) ইন্সটল করা ছিল। এই জন্য php এর আগে পিএইচপি এক্সটিউটেবলের path (/opt/lampp/bin/) প্রিফিক্স করে দিতে হবে।

```
$ /opt/lampp/bin/php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
$ /opt/lampp/bin/php -r "if (hash_file('sha384', 'composer-setup.php') === '93b54496392c062774670ac18b134c3b3a95e5a5e5c8f1a9f115f203b75bf9a129d5daa8ba6a13e2cc8a1da0806388a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
$ /opt/lampp/bin/php composer-setup.php
$ /opt/lampp/bin/php -r "unlink('composer-setup.php');"
```

এবার প্রজেক্ট ফোল্ডারে নিচের কমান্ড দিয়ে কম্পোজার ইনিসিয়ালাইজ করলে প্রজেক্ট সম্পর্কে কিছু প্রশ্ন জিজ্ঞাসা করবে। একেবারে শেষে ঐ ফোল্ডারের মধ্যে composer.json নামে একটি ফাইল তৈরী হবে।

```
composer init
```

প্রজেক্ট সম্পর্কে যে সব তথ্য দিতে হবেঃ

```
Package name (<vendor>/<name>)
Description
Author
Minimum Stability
Package Type
License

Define your dependencies.

Would you like to define your dependencies (require) interactively [yes]?
Would you like to define your dev dependencies (require-dev) interactively [yes]?

Do you confirm generation [yes]?
```

এবার, composer.json ফাইলটি আমার পছন্দের editor এ ওপেন করে "require": {} এর পরে নীচের মত করে autoload এর কনফিগ উল্লেখ করে দিতে হবে।

```
"autoload": {
	"psr-4": { "Inc\\": "./inc }
}
```

এখানে composer কে বলা হচ্ছে যে, আমি psr-4 কনভেনসন ব্যবহার করব এবং আমার লাইব্রেরীগুলো সব inc ফোল্ডারের মধ্যে আছে।

এরপর, টার্মিনালে এসে নিচের কমান্ড দিলে Composer আমার জন্য আমার প্রজেক্ট ফোল্ডারের মধ্যে vendor নামে একটি ফোল্ডার তৈরী করে এর মধ্যে autoload.php ফাইল, composer নামে একটি ফোল্ডার এবং তার মধ্যে ইন্টারনালি ব্যবহারের জন্য কিছু অন্যান্য ফাইলও তৈরী করবে।

```
composer install
```

### সতর্কতা

vendor ফোল্ডারের মধ্যে থাকা কোন ফাইল পরিবর্তন করা যাবে না। প্রয়োজনে composer.json ফাইলে পরিবর্তন করতে হবে। পরিবর্তন করার পরে নিচের কমান্ডটি রান করলে vendor ফোল্ডারের মধ্যে থাকা ফাইলগুলো Composer নিজে পরিবর্তন করে নিবে।

```
composer dump-autoload
```
