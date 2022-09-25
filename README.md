# @ngx-translate/multi-webpack-loader 

A loader for [ngx-translate](https://github.com/ngx-translate/core) that loads translations using webpack imports of json files.


* [Installation](#installation)
* [Usage](#usage)
* [Tip](#tip)

## Installation

We assume that you already installed [ngx-translate](https://github.com/ngx-translate/core).

Now you need to install the npm module for `MultiWebpackLoader`:

```sh
npm install ngx-translate-multi-webpack-loader --save
```


## Usage
#### Setup the `TranslateModule` to use the `MultiWebpackLoader`:

The `MultiWebpackLoader` uses webpack imports of json files to load translations


```ts
import {NgModule} from '@angular/core';
import {BrowserModule} from '@angular/platform-browser';
import {TranslateModule, TranslateLoader} from '@ngx-translate/core';
import {MultiTranslateLoader} from "ngx-translate-multi-webpack-loader";
import {AppComponent} from "./app";



export class LazyTranslateLoader implements TranslateLoader {
  public getTranslation(lang: string): Observable<any> {
    return MultiTranslateLoader().getTranslation(I18NFiles(lang));
  }
} 

//It has to be an array of webpack import.
export function I18NFiles( lang: string) {
    return [
     import(`../assets/i18n/${lang}.json`),
     import(`../app/pages/my-project/assets/i18n/${lang}.json`),
    ]
}


@NgModule({
    imports: [
        BrowserModule,
        TranslateModule.forRoot({
            loader: {
                provide: TranslateLoader,
                useClass: LazyTranslateLoader
            }
        })
    ],
    bootstrap: [AppComponent]
})
export class AppModule { }
```
## Tip

For enable json import add 

```json
"compilerOptions": {
    ...
    "resolveJsonModule": true,
    "esModuleInterop": true,
    ...
}
```


in tsconfig.json file.

Love **ngx-translate-multi-webpack-loader** ? Give to repo a **star** :star:. 

