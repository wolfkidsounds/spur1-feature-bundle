# FeatureFlagBundle

The FeatureFlagBundle is a very KISS bundle to manage features flags in your Symfony
applications.

Just allow to know if a feature is enable or not. If you have more complex needs,
please considerer using an another solution like [Qandidate\Toggle](https://github.com/qandidate-labs/qandidate-toggle-bundle).

## Compatibility

This bundle is tested with Symfony 2.7+, but it should be compatible with
Symfony 2.3+.

## Documentation

### Install it

Install extension using [composer](https://getcomposer.org):

```json
{
    "require": {
        "novaway/feature-flag-bundle": "dev-master"
    }
}
```

Enable the bundle in your application `AppKernel`:

```php
<?php

public function registerBundles()
{
    $bundles = [
        // ...
        new Novaway\Bundle\FeatureFlagBundle\NovawayFeatureFlagBundle(),
    ];

    // ...

    return $bundles;
}
```

### Use it

#### Define your features

First you have to configure the bundle and define your feature flags in the `config.yml`.

```yaml
# ...
novaway_feature_flag:
    features:
        my_feature_1: false
        my_feature_2: true
```

#### As a service

The bundle add a `novaway_feature_flag.manager.feature` service you can use in your
PHP classes.

```php
class MyController extends Controller
{
    public function myAction()
    {
        $featureManager = $this->get('novaway_feature_flag.manager.feature');
        
        if ($featureManager->isEnabled('my_feature_1')) {
            // my_feature_1 is enabled
        }
        
        if ($featureManager->isDisabled('my_feature_2')) {
            // my_feature_2 is not enabled
        }
    }
}
```

#### In your Twig templates

You can also check a flag in your templates:

```twig
{% if isFeatureEnabled('my_feature_1') %}
    {% include 'feature1_template.html.twig' %}
{% endif %}

{% if isFeatureDisabled('my_feature_2') %}
    {% include 'feature2_template.html.twig' %}
{% endif %}
```

## License

This library is published under [MIT license](LICENSE)
