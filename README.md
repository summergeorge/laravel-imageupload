# Laravel Imageupload

Upload image using Laravel's build in function and resize it using [Imagine library](https://imagine.readthedocs.org/en/latest/) automatically.

## Compatibility

* [Laravel 5.x](https://github.com/matriphe/laravel-imageupload/blob/laravel5/README.md)
* Laravel 4.2

## Installation

Open `composer.json` and require this line below.

```json
"matriphe/imageupload": "4.2.*"
```

Or you can run this command from your project directory.

```bash
composer require "matriphe/imageupload:4.2.*"
```

### Laravel Installation

Open the `app/config/app.php` and add this line in `providers` section.

```php
'Matriphe\Imageupload\ImageuploadServiceProvider'
```

Still in `app/config/app.php`, add this line in `alias` section.

```php
'Imageupload' => 'Matriphe\Imageupload\ImageuploadFacade'
```

## Publish Configuration

To control the configuration, you have to *publish* the configuration file.

```bash
 php artisan config:publish matriphe/imageupload
```

After running this command, there will be `config/imageupload.php` file.

## Test It

After publishing the configuration file, you can set up a route and view.

The uploaded file will be saved in `public/uploads` directory. Of course, you can change this by publishing and modifying configuration file.

### Route Example

```php
<?php
// routes.php
...
Route::any('matriphe/imageupload', function() 
{
    $data = [];
    
    echo config('imageupload.library');
    
    if (Request::hasFile('file')) {
        $data['result'] = Imageupload::upload(Request::file('file'));
    }
    
    return view('form.blade.php')->with($data);
});
```

### View

Add this in your views directory.

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Imageupload</title>
    </head>
    <body>
        <form action="{{ URL::current() }}" method="post" enctype="multipart/form-data">
            <input type="hidden" name="_token" value="{{ Session::token() }}">
            <pre>{{ (!empty($result) ? print_r($result, 1) : '') }}</pre>
            <div>
                <input type="file" name="file">
            </div>
            <div>
                <button type="submit">Upload!</button>
            </div>
        </form>
    </body>
</html>
```

## Usage

Just use the `Imageupload::upload($file)` function and it will take care of cropping and renaming. Of course, you can modify on the fly by passing parameter `Imageupload::upload($filesource, $newfilename, $dir)`.

The return of the function is **array**.

### Example
```php
if (Request::hasFile('file')) {
    $result = Imageupload::upload(Request::file('file'));
}
```
### Output
```array
Array
(
    [path] => /Users/matriphe/www/laravel/4.2/public/uploads/images
    [dir] => uploads/images
    [original_filename] => Xiaomi Media Invitation Final.png
    [original_filepath] => /Users/matriphe/www/laravel/4.2/public/uploads/images/424370e1611a171b99b5c6ec20aaeedf.png
    [original_extension] => png
    [original_filesize] => 129840
    [original_mime] => image/png
    [filename] => 424370e1611a171b99b5c6ec20aaeedf.png
    [original_filedir] => uploads/images/424370e1611a171b99b5c6ec20aaeedf.png
    [basename] => 424370e1611a171b99b5c6ec20aaeedf
    [original_width] => 1281
    [original_height] => 816
    [dimensions] => Array
        (
            [square50] => Array
                (
                    [path] => /Users/matriphe/www/laravel/4.2/public/uploads/images
                    [dir] => uploads/images
                    [filename] => 424370e1611a171b99b5c6ec20aaeedf_square50.png
                    [filepath] => /Users/matriphe/www/laravel/4.2/public/uploads/images/424370e1611a171b99b5c6ec20aaeedf_square50.png
                    [filedir] => uploads/images/424370e1611a171b99b5c6ec20aaeedf_square50.png
                    [width] => 50
                    [height] => 50
                    [filesize] => 3683
                )

            [square100] => Array
                (
                    [path] => /Users/matriphe/www/laravel/4.2/public/uploads/images
                    [dir] => uploads/images
                    [filename] => 424370e1611a171b99b5c6ec20aaeedf_square100.png
                    [filepath] => /Users/matriphe/www/laravel/4.2/public/uploads/images/424370e1611a171b99b5c6ec20aaeedf_square100.png
                    [filedir] => uploads/images/424370e1611a171b99b5c6ec20aaeedf_square100.png
                    [width] => 100
                    [height] => 100
                    [filesize] => 10734
                )

            [square200] => Array
                (
                    [path] => /Users/matriphe/www/laravel/4.2/public/uploads/images
                    [dir] => uploads/images
                    [filename] => 424370e1611a171b99b5c6ec20aaeedf_square200.png
                    [filepath] => /Users/matriphe/www/laravel/4.2/public/uploads/images/424370e1611a171b99b5c6ec20aaeedf_square200.png
                    [filedir] => uploads/images/424370e1611a171b99b5c6ec20aaeedf_square200.png
                    [width] => 200
                    [height] => 200
                    [filesize] => 35609
                )

            [square400] => Array
                (
                    [path] => /Users/matriphe/www/laravel/4.2/public/uploads/images
                    [dir] => uploads/images
                    [filename] => 424370e1611a171b99b5c6ec20aaeedf_square400.png
                    [filepath] => /Users/matriphe/www/laravel/4.2/public/uploads/images/424370e1611a171b99b5c6ec20aaeedf_square400.png
                    [filedir] => uploads/images/424370e1611a171b99b5c6ec20aaeedf_square400.png
                    [width] => 400
                    [height] => 400
                    [filesize] => 125267
                )

            [size50] => Array
                (
                    [path] => /Users/matriphe/www/laravel/4.2/public/uploads/images
                    [dir] => uploads/images
                    [filename] => 424370e1611a171b99b5c6ec20aaeedf_size50.png
                    [filepath] => /Users/matriphe/www/laravel/4.2/public/uploads/images/424370e1611a171b99b5c6ec20aaeedf_size50.png
                    [filedir] => uploads/images/424370e1611a171b99b5c6ec20aaeedf_size50.png
                    [width] => 50
                    [height] => 32
                    [filesize] => 2375
                )

            [size100] => Array
                (
                    [path] => /Users/matriphe/www/laravel/4.2/public/uploads/images
                    [dir] => uploads/images
                    [filename] => 424370e1611a171b99b5c6ec20aaeedf_size100.png
                    [filepath] => /Users/matriphe/www/laravel/4.2/public/uploads/images/424370e1611a171b99b5c6ec20aaeedf_size100.png
                    [filedir] => uploads/images/424370e1611a171b99b5c6ec20aaeedf_size100.png
                    [width] => 100
                    [height] => 64
                    [filesize] => 6700
                )

            [size200] => Array
                (
                    [path] => /Users/matriphe/www/laravel/4.2/public/uploads/images
                    [dir] => uploads/images
                    [filename] => 424370e1611a171b99b5c6ec20aaeedf_size200.png
                    [filepath] => /Users/matriphe/www/laravel/4.2/public/uploads/images/424370e1611a171b99b5c6ec20aaeedf_size200.png
                    [filedir] => uploads/images/424370e1611a171b99b5c6ec20aaeedf_size200.png
                    [width] => 200
                    [height] => 127
                    [filesize] => 21432
                )

            [size400] => Array
                (
                    [path] => /Users/matriphe/www/laravel/4.2/public/uploads/images
                    [dir] => uploads/images
                    [filename] => 424370e1611a171b99b5c6ec20aaeedf_size400.png
                    [filepath] => /Users/matriphe/www/laravel/4.2/public/uploads/images/424370e1611a171b99b5c6ec20aaeedf_size400.png
                    [filedir] => uploads/images/424370e1611a171b99b5c6ec20aaeedf_size400.png
                    [width] => 400
                    [height] => 255
                    [filesize] => 76487
                )

        )

)
```