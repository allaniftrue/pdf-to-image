# Convert a pdf to an image

This package provides an easy to work with class to convert pdf's to images.

## Requirements

You should have [Imagick](http://php.net/manual/en/imagick.setresolution.php) and [Ghostscript](http://www.ghostscript.com/) installed.

## Install

The package can be installed via composer:
``` bash
$ composer require allaniftrue/pdf-to-image
```

## Usage

Converting a pdf to an image is easy.

```php
$pdf = new Bnb\PdfToImage\Pdf($pathToPdf);
$pdf->saveImage($pathToWhereImageShouldBeStored);
```

If the path you pass to `saveImage` has the extensions  `jpg`, `jpeg`, or `png` the image will be saved in that format.
Otherwise the output will be a jpg.

## Other methods
You can get the total number of pages in the pdf:
```php
$pdf->getNumberOfPages(); //returns an int
```

By default the first page of the pdf will be rendered. If you want to render another page you can do so:
```php
$pdf->setPage(2)
    ->saveImage($pathToWhereImageShouldBeStored); //saves the second page
```

You can override the output format:
```php
$pdf->setOutputFormat('png')
    ->saveImage($pathToWhereImageShouldBeStored); //the output wil be a png, no matter what
```

You can configure custom settings (where page is the page number) :
```php
$beforeImageReadSettings = function (\Imagick $imagick, $page) {
    $imagick->setColorspace(\Imagick::COLORSPACE_SRGB);

    return $imagick;
};

$beforeImageWriteSettings = function (\Imagick $imagick, $page) {
    $imagick->resizeImage(1024, 1024, \Imagick::FILTER_LANCZOS, 0, true);
    $imagick->setImageColorspace(\Imagick::COLORSPACE_GRAY);

    return $imagick;
};

$pdf = new Pdf($this->testFile, $beforeImageReadSettings, $beforeImageWriteSettings)
    ->saveImage($pathToWhereImageShouldBeStored); //the output will be resized to a grayscale image with a best-fit dimension of 1024x1024
```

## Change log

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Testing

``` bash
$ composer test
```

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

## Security

If you discover any security related issues, please email support@bnb.be instead of using the issue tracker.

## Credits

- [B&B Web Expertise](https://github.com/allaniftrue)
- [Freek Van der Herten](https://github.com/spatie)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.