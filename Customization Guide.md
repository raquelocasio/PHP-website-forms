The PHP Website Forms Customization Guide
=====================================

When you download a form, the file "handler.php" already has a basic implementation ready for you. This guide explains how to customize handler.php.

See a video demo at [https://youtu.be/jAr4ZtLnmn0](https://youtu.be/jAr4ZtLnmn0)

Update your email address to receive form submission emails
------------------------------------

`$pp->sendEmailTo('someone@gmail.com'); // ← Your email here`

Replace someone@gmail.com with your email address.

If you want to send email to more than one email addresses, just enter it as an array like so:

`$pp->sendEmailTo(['someone@gmail.com', 'another@gmail.com','more@gmail.com']);` 

Adding Form Validations
------------------------------------

Add your validations in the validate() function. You can add more validations as required. Examples:

`$validator = $pp->getValidator();
$validator->fields(['name','email'])->areRequired()->maxLength(50);
$validator->field('email')->isEmail();
$validator->field('message')->maxLength(6000);`

Customizing PHPMailer
------------------------------------

The FormHandler uses [PHPMailer](https://github.com/PHPMailer/PHPMailer) to send emails. You can customize the internal PHPMailer object like so:

`$mailer = $pp->getMailer();
$mailer->setFrom('someone@yourwebsite.com','Form',false);`

Using an SMTP account
------------------------------------

You can customize PHPMailer to use an SMTP account too. The snippet below uses SMTP account from Amazon SES:

`$mailer = $pp->getMailer();`

`//Using Amazon AWS SES SMTP account
$mailer->IsSMTP();
$mailer->SMTPAuth   = true; 
$mailer->SMTPSecure = "tls"; 
$mailer->Host       = "email-smtp.us-east-1.amazonaws.com";
$mailer->Username   = "YOUR AWS SMTP CREDENTIALS";
$mailer->Password   = "YOUR AWS SMTP CREDENTIALS";`

`$mailer->setFrom('yourname@domain.com', 'Form');`

See the [PHPMailer](https://github.com/PHPMailer/PHPMailer) Page for more customization options.

File Uploads
------------------------------------

If you have file uploads in the form, just call attachFiles() with the name of the file input field to attach the file to the email.

`$pp->attachFiles(['image']);`
where 'image' is the name of the file upload field

Captcha
------------------------------------

You can use [Gregwar/Captcha](https://github.com/Gregwar/Captcha) to add captcha to your form. Call requireCaptcha() function so that the validation is triggered.

`$pp->requireCaptcha();`

ReCaptcha
------------------------------------

Alternative to the image captcha, you can add ReCaptcha to the form as well. First you have to signup with reCaptcha and get your secret key.
Then Enable ReCaptcha and setup your secret Key.

`$pp->requireReCaptcha();
$pp->getReCaptcha()->initSecretKey('Your ReCaptcha Secret Key Here');`
