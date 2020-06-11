# Create-react-app-multilangual-approach

Project setup

Get project through Git Clone

Use command :

git clone https://github.com/deepakdhamijaevry/Create-react-app-multilingual-approach.git

Use yarn or npm to install the project dependencies:

Using npm..
npm install

Using yarn..
yarn install

# Add react-intl to your project

# Step 1
As we want to use react-intl to localize our application, add it to you project:

npm install --save react-intl

# Step 2
Wrap your app with IntlProvider

To make the internationalization functions visible in all our components we have to wrap the App component with IntlProvider. 
It expects the current locale as property. For the moment we're setting it to a fixed language, later we will determine the user's locale by evaluating the language request sent by the browser.

import {IntlProvider} from "react-intl";

ReactDOM.render(

    <IntlProvider locale='en'>
    
        <App/>
        
    </IntlProvider>,
    
    document.getElementById('root')
    
);

# Step 3
Create folder "i18n" and its subfolder "locales" in src folder and add the language files as json

The translations of our custom text messages will be stored for each language in a separate .json file.Create the JSON file src/i18n/locales/nb.json for the Norwegion translation and create an en.json file english 

Add translated messages from JSON files:

en.json:

{

     "LOGIN.INVALIDLOGIN": "Invalid Email/Password"
     
}

nb.json:

{

     "LOGIN.INVALIDLOGIN": "Ugyldig e-postadresse / passord",
     
}

Import both .json files in one index.js in same folder and then export both the files

Index.js

import en from "./en.json";

import nb from "./nb.json";

export default { en, nb };


# Step 4

Add internationalization data with addLocaleData. In the first step we have to load the locale data for languages we want to support. 
This data is provided by react-intl. The locale data is added by calling addLocaleData().

Add these lines to app.js:

import { IntlProvider, addLocaleData } from "react-intl";

import translations from "../../i18n/locales";

const language = 'en'; //Default Language (english)

addLocaleData(require(`react-intl/locale-data/${language}`));


# Step 5

First import FormattedMessage at the top of the login.js components

import { FormattedMessage, injectIntl } from 'react-intl';

&lt;FormattedMessage id="LOGIN.TITLE" defaultMessage="Employee Portal"&gt;
