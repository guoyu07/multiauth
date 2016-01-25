# Laravel-5-MultiAuth
This package handles Multiple Authentication in Laravel 5 (Fork of Ollieread MultiAuth).
You can find the documentation <a href="http://saravanan.tomrain.com/multiauth-in-laravel-5-0/">here</a>

安装

1.先备份的你的代码

这个不多说，如果你不想在出错后悲剧的话。

2.打开根目录下的composer.json，加入你要安装的包：

"require": {
        "ollieread/multiauth": "dev-master"
}
3.更新composer

4.打开app/config/app.php 修改 AuthServiceProvider的配置
Illuminate\Auth\AuthServiceProvider
改成
Ollieread\Multiauth\MultiauthServiceProvider


使用

1.修改app/config/auth.php

return array(

  'driver' => 'eloquent',

  'model' => 'User',

  'table' => 'users',

  'reminder' => array(

    'email' => 'emails.auth.reminder',

    'table' => 'password_reminders',

    'expire' => 60,

  ),

);

替换成

return array(

  'multi' => array(
    'account' => array(
      'driver' => 'eloquent',
      'model' => 'Account'
    ),
    'user' => array(
      'driver' => 'database',
      'table' => 'users'
    )
  ),

  'reminder' => array(

    'email' => 'emails.auth.reminder',

    'table' => 'password_reminders',

    'expire' => 60,

  ),

);

2.

Auth::account()->attempt(array(
  'email'	 => $attributes['email'],
  'password'  => $attributes['password'],
));
Auth::user()->attempt(array(
  'email'	 => $attributes['email'],
  'password'  => $attributes['password'],
));
Auth::account()->check();
Auth::user()->check();
