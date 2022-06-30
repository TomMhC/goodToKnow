# Angular Flex-Layout

## Source

- [GitHub - angular/flex-layout: Provides HTML UI layout for Angular applications; using Flexbox and a Responsive API](https://github.com/angular/flex-layout)

- [Angular Flex-Layout Demos](https://tburleson-layouts-demos.firebaseapp.com/#/docs)

## Install

```shell
npm install @angular/flex-layout @angular/cdk --save
```

## Usage

```ts
import { FlexLayoutModule } from '@angular/flex-layout';

@NgModule({
  declarations: [
  ],
  imports: [
    FlexLayoutModule
  ],
  providers: []
})
export class AppModule { }

```

```html
<div fxLayout="column">
  <div fxLayout="row wrap" fxLayoutGap="1em">
    <div fxFlex="25%" fxFlex.lt-md="33%" class="card"> 1 </div>
    <div fxFlex="25%" fxFlex.lt-md="33%" class="card"> 2 </div>
    <div fxFlex="25%" fxFlex.lt-md="33%" class="card"> 3 </div>
    <div fxFlex="25%" fxFlex.lt-md="33%" class="card"> 4 </div>
  </div>
  <div fxLayout="row wrap">
    <div fxFlex="25%" fxFlex.lt-lg="50%" class="card"> A </div>
    <div fxFlex="25%" fxFlex.lt-lg="50%" class="card"> B </div>
    <div fxFlex="25%" fxFlex.lt-lg="50%" class="card"> C </div>
    <div fxFlex="25%" fxFlex.lt-lg="50%" class="card"> D </div>
  </div>
</div>
```
