# Yii2 image thumbnail

Create image thumbnails use Imagine. Thumbnail created and cached automatically.
It allows you to create placeholder with service [http://placehold.it/](http://placehold.it/) or holder.js.

#### Features:
- Easy to use
- Use Imagine
- Automaticly thumbnails caching
- Cache sorting to subdirectories
- Caching placeholder from URL (placehold.it)
- Random color
- Use placehold.it & holder.js

## Installation

### Composer

The preferred way to install this extension is through [Composer](http://getcomposer.org/).

Either run ```php composer.phar require sadovojav/yii2-image-thumbnail "dev-master"```

or add ```"sadovojav/yii2-image-thumbnail": "dev-master"``` to the require section of your ```composer.json```

### Config

Attach the component in your config file:

```php
'bootstrap' => [
    'thumbnail',
],

'components' => [
    'thumbnail' => [
        'class' => 'sadovojav\image\Thumbnail',
    ],
],
```

#### Parameters
- string `basePath` = `@webroot` - Base path
- string `cachePath` = `@runtime/thumbnails` - Cache path alias
- integer `cacheExpire` = `604800` - Cache expire time
- array `options` - other options (placeholder & quality)

#### Default options:

```php
'options' => [
    'placeholder' => [
        'type' => sadovojav\image\Thumbnail::PLACEHOLDER_TYPE_URL,
        'backgroundColor' => '#f5f5f5',
        'textColor' => '#cdcdcd',
        'text' => 'Ooops!',
        'random' => false
        'cache' => true
    ],
    'quality => 92
]
```

#### Attention
```
Cache only: PLACEHOLDER_TYPE_URL
If both "random" and "cache" are enabled, each colour will be cached
```

#### Placeholder type
- 1. sadovojav\image\Thumbnail::PLACEHOLDER_TYPE_JS - holder.js
- 2. sadovojav\image\Thumbnail::PLACEHOLDER_TYPE_URL - get placeholder by url

## Using

### Get cache image
```php
echo Yii::$app->thumbnail->img($file, $params, $options);
```
This method returns Html::img()

#### Parameters
- string `$file` required - Image file path
- array `$params` - Image manipulation methods. See Methods
- array `$options` - options for Html::img()

#### For example:
```php
<?= Yii::$app->thumbnail->img(IMAGE_SRC, [
    'thumbnail' => [
        'width' => 320,
        'height' => 230,
    ],
    'placeholder' => [
        'width' => 320,
        'height' => 230
    ]
]); ?>
```

### Get cache image url
```php
echo Yii::$app->thumbnail->url($file, $params);
```
This method returns cache image url

#### Parameters
- string `$file` required - Image file path
- array `$params` - Image manipulation methods. See Methods

#### For example:
```php
<?= Yii::$app->thumbnail->url(IMAGE_SRC, [
    'thumbnail' => [
        'width' => 320,
        'height' => 230,
    ],
    'placeholder' => [
        'width' => 320,
        'height' => 230
    ]
]); ?>
```

### Get placeholder image
```php
echo Yii::$app->thumbnail->placeholder($params, $options);
```
This method returns Html::img()

#### Parameters
- array `$params` required - Placeholder options. See Placeholder method
- array `$options` - options for Html::img()

#### For example:
```php
<?= Yii::$app->thumbnail->placeholder([
    'width' => 320,
    'height' => 230
]); ?>
```

## Method

### Resize
```php
'resize' => [
    'width' => 320,
    'height' => 200
]
```
#### Parameters
- integer `width` required - New width
- integer `height` required - New height

### Crop
```php
'crop' => [
    'width' => 250,
    'height' => 200,
]
```
#### Parameters
- integer `width` required - New width
- integer `height` required - New height
- integer `x` = `0` - X start crop position
- integer `y` = `0` - Y start crop position

### Thumbnail
```php
'thumbnail' => [
    'width' => 450,
    'height' => 250,
]
```
#### Parameters
- integer `width` required - New width
- integer `height` required - New height
- string `mode` = `THUMBNAIL_OUTBOUND` - Thumbnail mode `THUMBNAIL_OUTBOUND` or `THUMBNAIL_INSET`

### Placeholder
```php
'placeholder' => [
    'width' => 450,
    'height' => 250,
]
```
This method return image placeholder if image file doesn't exist.

#### Parameters
- integer `width` required - Placeholder image width
- integer `height` required - Placeholder image height
- string `backgroundColor` = `#f5f5f5` - Background color
- string `textColor` = `#cdcdcd` - Text color
- string `text` = `Ooops!` - Text
- string `random` = `false` - Random color
- string `cache` = `true` - Cache placeholder


#### Attention
```
Cache only: PLACEHOLDER_TYPE_URL
If both "random" and "cache" are enabled, each colour will be cached
```