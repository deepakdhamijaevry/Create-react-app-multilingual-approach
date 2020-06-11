# Create-react-app-multilangual-approach

# Project setup

Get project through Git Clone

Use command :

git clone https://github.com/deepakdhamijaevry/Create-react-app-multilingual-approach.git

Use yarn or npm to install the project dependencies:

# Using npm..

npm install

# Or using yarn..

yarn install

# Step 1
# Add react-intl to your project

Adding React Intl
To start using React Intl we need to add it to our project:

# Add with npm
npm install react-intl
# or add with yarn
yarn add react-intl

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
This data is provided by react-intl.

Add these lines to app.js:

import { IntlProvider, addLocaleData } from "react-intl";

import translations from "../../i18n/locales";

const language = 'en'; //Default Language (english)

# Step 5
The locale data is added by calling addLocaleData() in constructor and selected default language on load and added the languages array in state for dropdownlist control

  constructor() {
  
    super();
    
    this.state = {
    
      language: language,
      
      messages: translations[language],
      
      languages: [
        { value: 'en', name: 'English' },
        { value: 'nb', name: 'Norwegian' }
      ]
      
      //Default Language (en or nb -> as of now)
    }
    addLocaleData(require(`react-intl/locale-data/${language}`));
    
    this.languageChange = this.languageChange.bind(this);
    
  }
  
 # Step 6
Create function for choosing the particular language from dropdownlist and load the corresponsing language file

    languageChange(e) {
    let self = this;
    this.language = e.target.value;
    self.setState({
      language: this.language,
      messages: translations[this.language]
    });
    addLocaleData(require(`react-intl/locale-data/${this.language}`));
  }

# Step 7

First import FormattedMessage at the top of the login.js components

import { FormattedMessage, injectIntl } from 'react-intl';

&lt;FormattedMessage id="LOGIN.TITLE" defaultMessage="Employee Portal"&gt;
