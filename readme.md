# Files Sharing

<p align="center"><img src="https://github.com/axeloz/filesharing/raw/master/public/img/capture.png" width="700" /></p>

Powered by Laravel
<p><img src="https://laravel.com/assets/img/components/logo-laravel.svg"></p>

## Description

This PHP application based on Laravel 5.4 allows to share files like Wetransfer. You may install it **on your own server**. It **does not require** any database system, it works with JSON files into the storage folder. It is **multilingual** and comes with english and french translations for now. You're welcome to help translating the app.

It comes with a droplet. You may drag and drop some files or directories into the droplet, your files will be uploaded to the server as a bundle.

A bundle is like a package containing is a various number of files. The bundle has a 2 weeks expiry date after the creation of the bundle. This value is not editable yet, this is a todo.

This application provides three links per upload bundle :
- a bundle preview link : you can send this link to your recipients who will see the bundle content. For example: http://yourdomain/bundle/dda2d646b6746b96ea9b?auth=965242. The recipient can see all the files of the bundle, can download one given file only or the entire bundle.
- a bundle download link : you can send this link yo your recipients who will download all the files of the bundle at once (without any preview). For example: http://yourdomain/bundle/dda2d646b6746b96ea9b/download?auth=965242.
- a deletion link : for you only, it invalidates the bundle. For example:
http://yourdomain/bundle/dda2d646b6746b96ea9b/delete?auth=ace6f22f5.

Each of these links comes with an authorization code. This code is the same for the preview and the download links. However it is  different for the deletion link for obvious reasons.

The application also comes with a Laravel Artisan command as a background task who will physically remove expired bundle files of the storage disk. This command is configured to run every five minutes among the Laravel scheduled commands.

Sorry about the design, I'm not very good at this, you're welcome to help and participate.

## Features

- upload one or more files via drag and drop or via browsing your computer
- creation of a bundle
- ability to keep adding files to the bundle until you close your browser tab, the preview link remain untouched
- bundle expiration after 2 weeks
- sharing link with bundle content preview
- ability to download a single file of the bundle or the entire bundle
- direct download link (doesn't preview the bundle content)
- deletion link for bundle owner
- garbage collector which removes the expired bundles as a background task
- multilingual (EN and FR)
- easy installation, no database required
- upload limitation based on client IP filtering
- secured by tokens, authentication codes and non-publicly-accessible files
- (very) early stage for theming support

## Requirements

Basically, nothing more than Laravel itself:
- PHP >= 5.6.4
- OpenSSL PHP Extension
- PDO PHP Extension
- Mbstring PHP Extension
- Tokenizer PHP Extension
- XML PHP Extension

Plus:
- JSON PHP Extension (included in PHP 5.2+)
- ZipArchive PHP Extension (included in PHP 5.3+)

The application also uses:
- http://www.dropzonejs.com/
- http://jquery.com/
- https://clipboardjs.com/

## Installation

- configure your domain name. For example: files.yourdomain.com
- clone the repo or download the sources into the webroot folder
- configure your webserver to point your domain name to the public/ folder
- run a `composer install`
- run a `npm install --production`
- make sure that the PHP process has write permission on the ./storage folder
- generate the Laravel KEY: `php artisan key:generate`
- start the Laravel scheduler (it will delete expired bundles of the storage). For example `* * * * * php /path-to-your-project/artisan schedule:run >> /dev/null 2>&1`

Use your browser to navigate to your domain name (example: files.yourdomain.com) and **that's it**.

## Configuration

In order to configure your application, copy the .env.example file into .env. Then edit the .env file.

| Configuration | Description |
| ------------- | ----------- |
| `APP_ENV`     | change this to `production` when in production (`local` otherwise) |
| `APP_DEBUG` | change this to `false` when in production (`true` otherwise) |
| `TIMEZONE` | change this to your current timezone |
| `LOCALE` | change this to "fr" or "en" |
| `STORAGE_PATH` | (*optional*) changes this wherever you want to store the files. When missing, using the `storage` folder at the root of the application |
| `UPLOAD_MAX_FILES` | (*optional*) maximal number of files per bundle |
| `UPLOAD_MAX_FILESIZE` | (*optional*) change this to the value you want (K, M, G, T, ...). Attention : you must configure your PHP settings too (`post_max_size`, `upload_max_filesize` and `memory_limit`). When missing, using PHP lowest configuration |
| `UPLOAD_LIMIT_IPS` | (*optional*) a comma separated list of IPs from which you may upload files. Different formats are supported : Full IP address (192.168.10.2), Wildcard format (192.168.10.*), CIDR Format (192.168.10/24 or 1.2.3.4/255.255.255.0) or Start-end IP (192.168.10.0-192.168.10.10). When missing, filtering is disabled. |
| `APP_NAME`    | the title of the application |

## Development

If your want to modify the sources, you can use the Laravel Mix features:
- configure your domain name. For example: files.yourdomain.com
- clone the repo or download the sources into the webroot folder
- configure your webserver to point your domain name to the public/ folder
- run a `composer install`
- run a `npm install`
- run a `npm run watch` in order to recompile the assets when changed

## Roadmap / Ideas / Improvements

There are many ideas to come. You are welcome to **participate**.
- ability to define a bundle name and/or description that will be shown to the recipients
- make the expiry date editable per bundle
- limit upload permission by a password (or passwords)
- disable bundle after X downloads (value to be configurable by the bundle owner)
- ability to send link to recipients directly from the app
- add PHP unit testing
- more testing on heavy files
- customizable / white labeling (logo, name, terms of service, footer ...)
- responsiveness (is it really useful?)

## Licence

GPLv3

| Permissions     | Conditions                    | Limitations |
| --------------- | ----------------------------- | ----------- |
| Commercial use  | Disclose source               | Liability   |
| Distribution    | License and copyright notice  | Warranty    |
| Modification    | Same license                  |             |
| Patent use      |  State changes                |             |
| Private use     |                               |             |

https://choosealicense.com/licenses/gpl-3.0/

## Welcome on board

If you are willing to **participate** or if you just want to talk with me : sharing@mabox.eu
