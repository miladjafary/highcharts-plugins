#<3>Highcharts Localization plugin.</h3>
This plugin used for localization Highcharts date and number and also could be extend as you need.

#<h3>Installation</h3>
Installing this plugin is simple. just import Highchart plugin and jQuery as core modules and then first
import <code>jalai.js</code> then import <code>highcharts-localization.js</code> 

```javascript
    <script src="http://code.jquery.com/jquery-1.10.2.min.js"></script>
    <script src="http://code.highcharts.com/highcharts.js"></script>
    <script src="js/jalali.js"></script>
    <script src="js/highcharts-localization.js"></script>
```


By default persian date and number are include in <code>highcarts-localization.js</code>.for add new localization you should
below following steps:

- Create a json config object for converting Gregorian timestamp to your local date(e.g : Persian date).

    <strong>Important notes</strong>

    - You need a function that called <code>getDate</code> that accept timestamp parameter and return following parameters
    as a json config object :
    
    
```javascript
    return {
        date: date,
        hours: date.getHours(),
        day: date.getJalaliDay(),
        dayOfMonth: date.getJalaliDate(),
        month: date.getJalaliMonth(),
        fullYear: date.getJalaliFullYear()
    };
        
```
<strong>Example : </strong> 
```javascript
    var PersianLocalizationDate = {
        /**
         * Get a timestamp and return jalali date.
         * @param timestamp
         * @returns {{date: Date, hours: number, day: *, dayOfMonth: *, month: *, fullYear: *}}
         */
        getDate: function (timestamp) {
            var date = new Date(timestamp);
            return {
                date: date,
                hours: date.getHours(),
                day: date.getJalaliDay(),
                dayOfMonth: date.getJalaliDate(),
                month: date.getJalaliMonth(),
                fullYear: date.getJalaliFullYear()
            };
        }
    };
```

- Create following javascript config object and assign your localization json date converter
    (in our example <code>PersianLocalizationDate</code>) to date parameter.

<strong>Example : </strong>
```javascript
    return {
         /**
          * @type {String} , An ISO 639-1 language code(e.g :fa)
          */
         lang: '',
         /**
          * @type {String} , An ISO 3166-1 language code(e.g: IR)
          */
         country: '',
         date: PersianLocalizationDate,
         i18n: {
             weekdays: ['شنبه', 'یکشنبه', 'دوشنبه', 'سه شنبه', 'چهارشنبه', 'پنج شنبه', 'جمعه'],
             months: ['فروردین', 'اردیبهشت', 'خرداد', 'تیر', 'مرداد', 'شهریور', 'مهر', 'آبان', 'آذر', 'دی', 'بهمن', 'اسفند']
         }
    };
    
```
- Finally set <code>locale</code> option to Highcharts global options by <code>Highcharts.setOptions()</code>.

<strong>Final Example :</strong>
```javascript
    var PersianLocalizationDate = {
        /**
         * Get a timestamp and return jalali date.
         * @param timestamp
         * @returns {{date: Date, hours: number, day: *, dayOfMonth: *, month: *, fullYear: *}}
         */
        getDate: function (timestamp) {
            var date = new Date(timestamp);
            return {
                date: date,
                hours: date.getHours(),
                day: date.getJalaliDay(),
                dayOfMonth: date.getJalaliDate(),
                month: date.getJalaliMonth(),
                fullYear: date.getJalaliFullYear()
            };
        }
    };

    Highcharts.setOptions({
        locale: {
            /**
             * @type {String} , An ISO 639-1 language code
             */
            lang: 'fa',
            /**
             * @type {String} , An ISO 3166-1 language code
             */
            country: 'IR',
            date: PersianLocalizationDate,
            i18n: {
                weekdays: ['شنبه', 'یکشنبه', 'دوشنبه', 'سه شنبه', 'چهارشنبه', 'پنج شنبه', 'جمعه'],
                months: ['فروردین', 'اردیبهشت', 'خرداد', 'تیر', 'مرداد', 'شهریور', 'مهر', 'آبان', 'آذر', 'دی', 'بهمن', 'اسفند']
            }
        }
    });
```
- Know you can use blow functions for localization date and number :
    <ul>
        <li>
            <code>Highcharts.localizationDateFormat(dateFormat, timestamp) </code> :
            <div>Convert Gregorian date to your localization date, for example jalali date</div>
        </li>
        <li>
            <code>Highcharts.localizationNumber (number) </code> :
            <div>Convert english number to persian and arabic number</div>
        </li>
    </ul>

<h3><a href="http://jsfiddle.net/KjsY2/">See online example</a></h3>

Enjoy Highcharts localization.
Please contact me if there is any problem
Thanks all.

Milad Jafary (milad.jafary@gmail.com)

