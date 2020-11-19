# BUILD FOR ACCESSIBILITY WITH ANGULAR

* **Date**: Wednesday, November 18th, 2020 \| 10:00 AM - 5:00 PM Mountain Time.
* **GitHub**: [https://github.com/M2D2co/build-for-accessibility-with-angular/blob/main/requirements.md](https://github.com/M2D2co/build-for-accessibility-with-angular/blob/main/requirements.md)
* **Recordings**:

## Notes

![](../.gitbook/assets/image%20%28247%29.png)

Accesibility is the ability to perceive, understand, navigate, and interact with the web.

Imparment -&gt;  disability -&gt; handicap are things that affect accessibility

![](../.gitbook/assets/image%20%28254%29.png)

#### Categories of impairments:

* Auditory
* Visibility
* Physical
* Cognitive and Neurological
* Speech

These can be Permanent, Temporary and Situational



![](../.gitbook/assets/image%20%28230%29.png)

![](../.gitbook/assets/image%20%28240%29.png)

![](../.gitbook/assets/image%20%28231%29.png)

![](../.gitbook/assets/image%20%28237%29.png)

Accessibility should make the site easier to use.

Language

![](../.gitbook/assets/image%20%28246%29.png)

![](../.gitbook/assets/image%20%28233%29.png)

![](../.gitbook/assets/image%20%28262%29.png)

![](../.gitbook/assets/image%20%28242%29.png)

### Angular and Material



![](../.gitbook/assets/image%20%28252%29.png)

![](../.gitbook/assets/image%20%28263%29.png)

![](../.gitbook/assets/image%20%28257%29.png)



### Material Theming

![](../.gitbook/assets/image%20%28261%29.png)

![](../.gitbook/assets/image%20%28236%29.png)

![](../.gitbook/assets/image%20%28255%29.png)

![](../.gitbook/assets/image%20%28235%29.png)

Make sure the custom color pass the contrast

![](../.gitbook/assets/image%20%28258%29.png)

![](../.gitbook/assets/image%20%28249%29.png)

### Forms

![](../.gitbook/assets/image%20%28269%29.png)

![](../.gitbook/assets/image%20%28253%29.png)

![](../.gitbook/assets/image%20%28224%29.png)

![](../.gitbook/assets/image%20%28226%29.png)

![](../.gitbook/assets/image%20%28270%29.png)

![](../.gitbook/assets/image%20%28223%29.png)

### Actions

![](../.gitbook/assets/image%20%28268%29.png)

![](../.gitbook/assets/image%20%28264%29.png)

![](../.gitbook/assets/image%20%28244%29.png)

![](../.gitbook/assets/image%20%28229%29.png)

![](../.gitbook/assets/image%20%28248%29.png)

![](../.gitbook/assets/image%20%28267%29.png)

![](../.gitbook/assets/image%20%28265%29.png)

### Images

![](../.gitbook/assets/image%20%28239%29.png)

![](../.gitbook/assets/image%20%28260%29.png)

![](../.gitbook/assets/image%20%28227%29.png)

![](../.gitbook/assets/image%20%28243%29.png)

![](../.gitbook/assets/image%20%28238%29.png)

![](../.gitbook/assets/image%20%28225%29.png)























## Learnings

* Componenent naming and structure should help with Semantic HTML and Landmarks  
  I have use a post fix on the name instead of changing the `component`. e.g.

  home-page.component.ts

*  side-navigation.component.ts 
* user-dialog.component.ts
*  user-details-section.component.ts
* There is an accesibility tb in chrome when inspecting elements

![](../.gitbook/assets/image%20%28250%29.png)

* Add tests for accessibility:

![](../.gitbook/assets/image%20%28259%29.png)

* Wave can be used to see the page structure

![](../.gitbook/assets/image%20%28266%29.png)

* For Angular Material theming, make sure the custom color pass the contrast.  Angular theming guide: [https://material.angular.io/guide/theming](https://material.angular.io/guide/theming) Angular typography guide: [https://material.angular.io/guide/typography](https://material.angular.io/guide/typography) Google Fonts: [https://fonts.google.com/](https://fonts.google.com/) Webaim contrast checker: [https://webaim.org/resources/contrastchecker/](https://webaim.org/resources/contrastchecker/)  Color palette builder: [http://mcg.mbitson.com](http://mcg.mbitson.com)  Theme builder: [https://materialtheme.arcsine.dev/](https://materialtheme.arcsine.dev/) 

![](../.gitbook/assets/image%20%28271%29.png)

* Labels are only for form fields
* Axe provides nice information about the problem and how to fix it 

![](../.gitbook/assets/image%20%28234%29.png)

* It is better to have the button of type `submit` and the form call the `submit` method

![](../.gitbook/assets/image%20%28256%29.png)

* It is recommended to stack vertically label and inputs
* Prefer to enable/disable instead of hiding and showing based on an input
* Links are links. Buttons are buttons. Div and spans are not. Divs and spans are not focusable, disablebal, etc.
* For Link with icons, use the `aria-hidden="true"` and add a label

![](../.gitbook/assets/image%20%28228%29.png)

* You should always have `alt` tags on images, however it can be blank. The `alt` should describe what the image is trying to convey. Decorative images can have an empty `alt` or have a `role="presentation"`
* Accessiblity insights tool from microsoft is really good  

![](../.gitbook/assets/image%20%28245%29.png)

![](../.gitbook/assets/image%20%28241%29.png)

* Use `role="alert"` for status and `aria-live="polite"` for status notifcaiont and `aria-live="assertive"` for something that requires attention 

### 



