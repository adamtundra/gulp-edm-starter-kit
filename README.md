
# eDM Starter Kit

Includes a sass version of Ink (http://zurb.com/ink/docs.php).


## Installation

```
bundle install
bower install
npm install
```

(Ruby and Bundler must be installed: `gem install bundler`)

Copy `credentials.example.json` to `credentials.json` and enter any relevant details.

## Dev

```
gulp
```

Starts a server with browsersync in the `/dist` directory: `http://localhost:3000` 

### Stylesheets

`/styles/styles.scss` is compiled to `/styles/styles.css` and `/styles/kinetic.scss` is compiled to `/styles/kinetic.css`.

There are 3 CSS files included in the `<head>` tag:

#### styles.css
These styles are are inlined into any HTML elements that match any ID/class inside the .css file.

#### kinetic.css *(optional)*
These styles are rendered as an inline `<style>` block in the `<head>` of the HTML. Any styles that take advantage of keyframes/animation or other CSS3 features should be rendered here. If inlined styles aren't required, feel free to remove the tag from the HTML.

#### data.css *(optional)*
This file is hosted externally and is not inlined anywhere on the page. It is used for pulling in dynamic pseudo element 'content' data from a server generated .css file. If dynamic data isn't required, feel free to remove this tag from the HTML.

### Templating

[nunjucks](https://mozilla.github.io/nunjucks/) is used as the templating language. This allows support for partials, variables, functions and offers more flexibility/organisation than regular HTML.

The master template file is `nunjucks/layout/master.nunj`. This base layout can be extended by your 'index' files which live in the root /nunjucks directory. These files include partials from the `nunjucks/partials` directory and components from the `nunjucks/components` directory. This gets compiled to `dist/.index.html` as the final HTML output.

#### Sumblime Nunjucks Highlighting

The nunjucks syntax highligher package in Sublime Text 3 throws an error. Select `Package Control: Add Repoisitory` in Sublime and add ` https://github.com/andres-risso/sublime-nunjucks.git` then install the new nunjucks package from this repo instead. 

### JSON Data

Global data is located inside a file called `data.json` stored in the root directory. Data can be added in this file and passed and printed in a .handlebars template file using the `{{firstName}}` syntax. You can use this file to store strings, image paths etc to keep the data and templating seperated from each other.

## Build

```
gulp build
```

CSS is inlined using Premailer
Images are optimised using Imagemin
HTML and images are saved to the `/dist` directory

## Testing

```
gulp test

gulp test --emails="email@tundra.com.au"
gulp test --emails="email1@tundra.com.au,email2@tundra.com.au"

gulp test --subject="..."
```

**S3**
Before sending a test to Litmus or an email address, all image are uploaded to S3 and all `images/` paths are changed in the html.

AWS credentials are set in `credentials.json`.

**Litmus**
If `gulp test` is called without the `emails` argument then it is sent to Litmus using the API. Subsequent tests are created as new versions not new tests.

Litmus API details are set in `credentials.json`.
Theres is also a complete list of all possible email clients for the `litmus.applications` array in `litmus_clients.json`.

**Email**
If `gulp test` is called with the `emails` argument then an email is sent to each comma-separated address provided using the Mailgun API.

Mailgun API details are set in `credentials.json`.

**Subject**
The email subject line is set in this order:

1. The `subject` argument passed to `gulp test`
2. The `subject` property in `package.json`
3. The `name` property in `package.json`

## MailChimp & Campaign Monitor Documentation

Campaign Monitor template language reference: https://www.campaignmonitor.com/create/

Mailchimp template language reference: http://templates.mailchimp.com/getting-started/template-language/
