# angularmoviefeed
Angular Moviefeed

## Table of Contents
* [Version](#version)
* [Important Note](#important-note)
* [Prerequisite Environment](#prerequisite-environment)
* [Generating Angular app with extra features](#generating-angular-app-with-extra-features)
* [Change Page Title](#change-page-title)
* [Change FavIcon](#change-favicon)
* [Setup the Angular project in Nginx conf file](#setup-the-angular-project-in-nginx-conf-file)
* [Modify the following files to change the custom uri](#modify-the–following-files-to-change-the-custom-uri)

### Version
* 0.0.1

### **Important Note**
* This script was written with Angular 13.2.5 methods on NodeJS 17.6.0

### Prerequisite Environment
* Install
  * NodeJS
    * Use the following web site to download for your operating system (Windows/Mac OS/Linux)
      * https://nodejs.org/
      * `node -v`
* Npm
  * `npm install -g npm@latest`
  * `npm -v`

### Generating Angular app with extra features
* Generate Angular App
  * Navigate to project
    * `cd /path/of/project/location/`
      * Execute any of the commands below
        * `ng new <project-name>`
          * Type Yes for routing
          * Choose SCSS
        * `ng new <project-name> --style=scss/css/... --skipTests --routing=true/false`
          * NOTE: A newer flag will be utilized from now on
            * `ng new <project-name> --style=scss/css/... --skiptests --routing=true/false`
          * **WAIT FOR THIS TO FINISH**
* Open Command Prompt without Administrator
  * Navigate to project
    * `cd /path/inside/parent/directory`
      * Serve Angular project (default HTTP host and port number)
        * `ng serve`
* Start Angular which opens in a web browser
  * `ng serve -o`
* Bootstrap (Make sure you are in the Angular project folder)
  * Install Bootstrap
    * `npm install --save bootstrap`
      * **WAIT FOR THIS TO FINISH**
  * Reconfigure the angular.json file to include the new bootstrap files
    * Open the angular.json file in the scripts section and add the two lines for bootstrap.
      * <pre>
          "styles": [
            "node_modules/bootstrap/dist/css/bootstrap.min.css",
          ],
          "scripts": [
            "node_modules/bootstrap/dist/js/bootstrap.min.js"
          ]
        </pre>
    * Save and exit
* FontAwesome
  * Install
    * `ng add @fortawesome/angular-fontawesome`
      * Would you like to proceed? Y
      * Select the following Free Icons
        * Free Solid Icons
        * Free Regular Icons
        * Free Brands Icons
        * Do not select the following Icons as they are not free to use
        * Pro Solid Icons    [ Requires: https://fontawesome.com/pro ]
        * Pro Regular Icons  [ Requires: https://fontawesome.com/pro ]
        * Pro Light Icons    [ Requires: https://fontawesome.com/pro ]
        * Pro Duotone Icons  [ Requires: https://fontawesome.com/pro ]
      * Click Enter
        * **WAIT FOR THIS TO FINISH**
  * Utilize the font awesome in your project add the following lines to your app.module.ts file. Your icons will differ from what is shown below.
    * <pre>
        import { FontAwesomeModule, FaIconLibrary } from '@fortawesome/angular-fontawesome';
        import { faBars as faBars } from '@fortawesome/free-solid-svg-icons';
        import { faTimes as faTimes } from '@fortawesome/free-solid-svg-icons';
        import { faHome as faHome } from '@fortawesome/free-solid-svg-icons';
        import { faPlus as faPlus } from '@fortawesome/free-solid-svg-icons';
        import { faSearch as faSearch } from '@fortawesome/free-solid-svg-icons';
        import { faInfo as faInfo } from '@fortawesome/free-solid-svg-icons';
        import { faEdit as faEdit } from '@fortawesome/free-solid-svg-icons';
        import { faSpinner as faSpinner } from '@fortawesome/free-solid-svg-icons';
        import { faTrashAlt as faTrashAlt } from '@fortawesome/free-solid-svg-icons';
        import { faThumbsUp as faThumbsUp } from '@fortawesome/free-solid-svg-icons';
        import { faThumbsDown as faThumbsDown } from '@fortawesome/free-solid-svg-icons';
        import { faExternalLinkAlt as faExternalLinkAlt } from '@fortawesome/free-solid-svg-icons';
        import { faFilm as faFilm } from '@fortawesome/free-solid-svg-icons';
      </pre>
  * Add the following lines of code to your app.module.ts file as well. Create a constructor function to retrieve the font awesome icon(s) of choice. Put the constructor into the export class AppModule section at the bottom of the page
    * <pre>
        // Add font awesome to the constructor
        constructor(library: FaIconLibrary) {
          // Adding the icons to be utilized throughout the web pages
          library.addIcons(faBars, faTimes, faHome, faInfo, faSearch, faPlus, faEdit, faSpinner, faTrashAlt, faThumbsUp, faThumbsDown, faExternalLinkAlt, faFilm);
        }
      </pre>
* Angular Material Package
  * `ng add @angular/material`
    * <pre>
        Would you like to proceed? (Y/n) Yes
        (You can customize the following color if the prebuilt colors do not meet your style)
        Choose a prebuilt theme name, or "custom" for a custom theme: (Use arrow keys) Pick either Indigo/Pink or Custom
        ❯ Indigo/Pink        [ Preview: https://material.angular.io?theme=indigo-pink ]
          Deep Purple/Amber  [ Preview: https://material.angular.io?theme=deeppurple-amber ]
          Pink/Blue Grey     [ Preview: https://material.angular.io?theme=pink-bluegrey ]
          Purple/Green       [ Preview: https://material.angular.io?theme=purple-green ]
          Custom
        ? Set up global Angular Material typography styles? (y/N) Yes
        ? Set up browser animations for Angular Material? (Y/n) Yes
      </pre>
    * The above will automatically be inserted into the angular.json file under the styles section of the file
      * `"./node_modules/@angular/material/prebuilt-themes/indigo-pink.css",`
* Install Material Datepicker and Time Picker Package
  * `npm install @angular-material-components/datetime-picker`
* Install Material Moment Adapter Package
  * `npm install @angular-material-components/moment-adapter`
* Utilize the Material Datepicker and Time Picker and Material Moment Adapter in your project, add the following lines to your app.module.ts file. Your settings will differ from what is shown below.
  * Add the following into the import section of the src/app/app.module.ts file
    * <pre>
        import { FormsModule, ReactiveFormsModule } from '@angular/forms';

        import { MatDatepickerModule } from '@angular/material/datepicker';
        import { MatInputModule } from '@angular/material/input';
        import { MatSelectModule } from '@angular/material/select';
        import { MatButtonModule } from '@angular/material/button';
        import { MatNativeDateModule } from '@angular/material/core';
        import { MatIconModule } from '@angular/material/icon';
        import { MatFormFieldModule } from '@angular/material/form-field';

        import { NgxMatMomentAdapter } from '@angular-material-components/moment-adapter';
        import {NgxMatDateFormats, NgxMatDatetimePickerModule, NgxMatNativeDateModule, NgxMatTimepickerModule, NGX_MAT_DATE_FORMATS, NgxMatDateAdapter } from '@angular-material-components/datetime-picker';

        Add the following customer date formats under the import section at the top
        // Setting custom date time display for date time pickers input field
        export const CUSTOM_DATE_FORMATS: NgxMatDateFormats = {
          parse: {
            dateInput: "YYYY-MM-DD HH:mm:ss"
          },
          display: {
            dateInput: "YYYY-MM-DD HH:mm:ss",
            monthYearLabel: "MMM YYYY",
            dateA11yLabel: "LL",
            monthYearA11yLabel: "MMMM YYYY"
          }
        };
      </pre>
  * Add the following to the NgModule import section
    * <pre>
        FormsModule,
        HttpClientModule,
        MatDatepickerModule,
        MatNativeDateModule,
        MatFormFieldModule,
        MatIconModule,
        MatInputModule,
        MatSelectModule,
        MatButtonModule,
        NgxMatDatetimePickerModule,
        NgxMatTimepickerModule,
        NgxMatNativeDateModule,
        ReactiveFormsModule
      </pre>
  * Add the following to the NgModule providers section towards the bottom of the page
    * <pre>
        {
          provide: NgxMatDateAdapter,
          useClass: NgxMatMomentAdapter,
        },
        {
          provide: NGX_MAT_DATE_FORMATS,
          useValue: CUSTOM_DATE_FORMATS
        }
      </pre>
* Include the following to your code to get date time picker displaying properly
  * Navigate to the .ts component of choice file and add the following to the import section
    * <pre>
        import { FormControl } from '@angular/forms';
      </pre>
  * Add the following to the export class component name section
    * <pre>
        public dateControl = new FormControl(new Date());
      </pre>
  * Navigate to the .html component of choice file and add the following to the html code
    * <pre>
        <mat-form-field>
          <input class="inputStyleDateTimePicker" matInput [ngxMatDatetimePicker]="picker" placeholder="Choose a date & time" [formControl]="dateControl">
          <mat-datepicker-toggle matSuffix [for]="$any(picker)"></mat-datepicker-toggle>
          <ngx-mat-datetime-picker #picker [showSpinners]="true" [showSeconds]="true" [stepHour]="1" [stepMinute]="1" [stepSecond]="1" [touchUi]="false" [enableMeridian]="false"
          [disableMinute]="false" [hideTime]="false"></ngx-mat-datetime-picker>
        </mat-form-field>
      </pre>
  * Navigate to the .css component of choice file and add the following to the css code
    * <pre>
        // Input field styling
        .mat-form-field {
          font-size: .3em;
        }

        // Date Time Picker input field style
        .inputStyleDateTimePicker {
          font-size: 3.5em;
        }

        // Input field icon styling
        .mat-datepicker-toggle {
          font-size: 3.5em;
        }
      </pre>

### Change Page Title
* Get the title to display for each component
  * Add the following line to the app.module.ts file
    * <pre>
        import { BrowserModule, Title } from '@angular/platform-browser';
      </pre>
  * Add the following to the NgModule providers section
    * <pre>
        Title
      </pre>
  * Add the following line to the component.ts of choice file
    * <pre>
        import { Title } from '@angular/platform-browser';
      </pre>
  * Add the following line in the export class section of the component.ts of choice file
    * <pre>
        title = 'Media Feed';
      </pre>
  * Add the following line in the export class constructor() parameter function of the component.ts of choice file
    * <pre>
        constructor(private titleService:Title) { }
      </pre>
  * Add the following line in the export class ngOnIntit() function of the component.ts of choice file
    * <pre>
        this.titleService.setTitle(this.title);
      </pre>

### Change FavIcon
* Overwrite the favicon.ico with your icon by replacing the file in src directory

### Setup the Angular project in Nginx conf file
* Open your nginx configuration of choice and add the following two sections to the file in your "server" section
  * <pre>
      location /<uri_name> {
        alias <path_to_angular_dist_project_folder>;
        autoindex off;
      }

      location ~ ^/<uri_name>(.*) {
        alias <path_to_angular_dist_project_folder>;
        try_files $1 $1/ /index.html =404;
      }
    </pre>
* Test and restart nginx if successful test
  * Test Nginx
    * `sudo nginx -t`
  * Restart Nginx Service
    * `sudo systemctl restart nginx`

### Modify the following files to change the custom uri
* If you have a specific URI that you are targeting, then proceed with the following modification
  * Navigate to the angular project src folder and locate the "<base href="">" line in src/index.html file
    * Change line
      * From
        * `<base href="/">`
      * To
        * `<base href="/<URL_Name>/">`

### Build Application for Production
* Navigate to project directory
  * `cd /path/inside/parent/directory`
    * Run ng build command in Angular CLI
      * To get the preview of the application, run the following command:
        * `ng serve --configuration production`
          * This starts a local HTTP server with production files. Navigate to http://localhost:4200/ to view the application.
      * Execute the following command to get the application ready for deployment
        * `ng build --configuration production`
          * If you get the following warning and or error message(s), then you will need to up the maximumWarning and or maximumError in the angular.json file.
            * "Warning: bundle initial exceeded maximum budget. Budget 500.00 kB was not met by 835.05 kB with a total of 1.30 MB.
            * Error: bundle initial exceeded maximum budget. Budget 1.00 MB was not met by 311.05 kB with a total of 1.30 MB."
          * Locate the "configurations" section in angular.json for your type of build (dev/stage/prod). Make the necessary changes to your angular.json file for the configuration build you are trying to execute and all should be fixed.
            * From
              * <pre>
                  "maximumWarning": "500kb",
                  "maximumError": "1mb"
                </pre>
            * To
              * <pre>
                  "maximumWarning": "2mb",
                  "maximumError": "2mb"
                </pre>
          * Save and Exit
