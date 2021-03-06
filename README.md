# sanatorium/mailer

Mailing extension for Cartalyst Platform

## Installation

### Composer

Add repository to your composer.json

    "repositories": [
      {
        "type": "composer",
        "url": "http://repo.sanatorium.ninja"
      }
    ]

Download the package

    composer require sanatorium/mailer

### Download

Download repository and copy it's contents to /extensions/sanatorium/mailer

## Documentation

Mailer is built to dispatch transactional emails when Event is triggered.

### Getting started

Let's imagine you want to send emails to customer and admin when order is placed.

#### Preparing template

After installation, open **Mailtransactions** menu and choose **+** icon to **Create new template**

The template for notification to admin would looks something like this:

    event: order.placed
    subject: New order was placed
    template: Hello admin!<br>New order was placed on your {{ config('platform.app.title') }} site<br>
    receivers: {{ config('platform.mail.from.address') }}

Let's assume our $order object contains customer's email in $order->customer_email, therefore we create new template with notification for customer like this:

    event: order.placed
    subject: Your order on {{ config('platform.app.title') }}
    template: Hello!<br>Thanks for your order!<br><br>Best regards,<br>{{ config('platform.app.title') }} site<br>
    receivers: {{ $order->customer_email }}

And then we trigger the event and pass data anywhere in the application like this:

    Event::fire('order.placed', ['order' => $order])

## Changelog

3.0.4 - 2016-09-15 - Platform 5 support, caching
1.2.3 - 2016-06-14 - Added common seed
1.1.0 - 2016-05-08 - Added simple documentation
1.0.0 - 2016-03-25 - Basic functionality

## Support

### Troubleshooting

**Q: No hint path defined for [sanatorium/mailer]**
A: This might be caused by barryvdh/laravel-debugbar. Set following collector to false to get rid of this error message:

    'debugbar.collectors.mail' => false