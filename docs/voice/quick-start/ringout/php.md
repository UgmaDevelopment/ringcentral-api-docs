no_breadcrumb:true

# RingOut PHP Quick Start

Welcome to the RingCentral Platform. RingCentral is the leading unified communications platform. From one system developers can integrate with, or build products around all the ways people communicate today: SMS, voice, fax, chat and meetings.

In this Quick Start, we are going to help you connect two people in a live phone call using our RingOut API, which dials two phone numbers, and then connects the two people when they answer. Let's get started.

## Create an App

The first thing we need to do is create an app in the RingCentral Developer Portal. This can be done quickly by clicking the "Create RingOut App" button below. Just click the button, enter a name and description if you choose, and click the "Create" button. If you do not yet have a RingCentral account, you will be prompted to create one.

<a target="_new" href="https://developer.ringcentral.com/new-app?name=RingOut+Quick+Start+App&desc=A+simple+app+to+demo+placing+a+Call+on+RingCentral&public=false&type=ServerOther&carriers=7710,7310,3420&permissions=RingOut&redirectUri=" class="btn btn-primary">Create RingOut App</a>
<a class="btn-link btn-collapse" data-toggle="collapse" href="#create-app-instructions" role="button" aria-expanded="false" aria-controls="create-app-instructions">Show detailed instructions</a>

<div class="collapse" id="create-app-instructions">
<ol>
<li><a href="https://developer.ringcentral.com/login.html#/">Login or create an account</a> if you have not done so already.</li>
<li>Go to Console/Apps and click 'Create App' button.</li>
<li>Give your app a name and description, then click Next.</li>
<li>On the second page of the create app wizard enter the following:
  <ul>
  <li>Select 'Private' for Application Type.</li>
  <li>Select 'Server-only (No UI)' for Platform Type.</li>
  </ul>
</li>
<li>On the third page of the create app wizard, select the following permissions:
    <ul>
      <li>RingOut</li>
    </ul>
</li>
<li>We are using Password Flow authentication, so leave "OAuth Redirect URI" blank.</li>
</ol>
</div>

When you are done, you will be taken to the app's dashboard. Make note of the Client ID and Client Secret. We will be using those momentarily.

## Place a Call

<h3>Install RingCentral PHP SDK</h3>

<pre>
  <code>
    curl -sS https://getcomposer.org/installer | php
    php composer.phar require ringcentral/ringcentral-php
  </code>
</pre>

<h3>Create and Edit ringout.py</h3>

<p>Create a file called <tt>ringout.py</tt>. Be sure to edit the variables in ALL CAPS with your app and user credentials. Be sure to also set the recipient's phone number.</p>

<pre><code>from ringcentral import SDK

$RECIPIENT = '&lt;ENTER PHONE NUMBER>'

$RINGCENTRAL_CLIENTID = '&lt;ENTER CLIENT ID>'
$RINGCENTRAL_CLIENTSECRET = '&lt;ENTER CLIENT SECRET>'
$RINGCENTRAL_SERVER = 'https://platform.devtest.ringcentral.com'

$RINGCENTRAL_USERNAME = '&lt;YOUR ACCOUNT PHONE NUMBER>'
$RINGCENTRAL_PASSWORD = '&lt;YOUR ACCOUNT PASSWORD>'
$RINGCENTRAL_EXTENSION = '&lt;YOUR EXTENSION, PROBABLY "101">'

$rcsdk = new RingCentral\SDK\SDK($RINGCENTRAL_CLIENTID, $RINGCENTRAL_CLIENTSECRET, $RINGCENTRAL_SERVER);

$platform = $rcsdk->platform();
$platform->login($RINGCENTRAL_USERNAME, $RINGCENTRAL_EXTENSION, $RINGCENTRAL_PASSWORD);

$platform->post('/account/~/extension/~/ring-out',
      array(
         'from' => array ('phoneNumber' => $RINGCENTRAL_USERNAME),
         'to' => array('phoneNumber' => $RECIPIENT),
         'playPrompt' => false
       ));
</code></pre>

<h3>Run Your Code</h3>

<p>You are almost done. Now run your script.</p>

<pre><code class="bash">$ php ringout.php
</code></pre>

## Publish Your App

Congratulations on creating your first RingCentral application. The last step is to publish your application. We recommend [going through this process](../basics/publish) for your first application so you can understand the steps to take in the future, but also to come to appreciate the care taken by RingCentral to ensure that only high-quality apps are allowed into our production environment.