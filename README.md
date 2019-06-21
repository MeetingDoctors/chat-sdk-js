This project was bootstrapped by MeetindDoctors on top o a [Create React App](https://github.com/facebook/create-react-app).

# Available integration options

This SDK consist in a Vanilla JS library that will, ultimately, render the MeetingDoctors web client on the integrators page.

For the integrator it will be necessary to integrate the JS, and also a custom CSS file to override the applied styles.

## `JavaScript`
#### `- <script src=widged.meetingdoctors.com/Vx.x.x/main.js />`

The first option to import the JS would be to insert a scrtipt on the HTML document pointing to the aimed version.
This would expose a new object (the library) attached at the Window object

You can call the methods then, in the following way

```javascript
<script>
window.meetingDoctors.initialize({...args});
...
</script>
```

See below the definition of those args

<!--Where mountPoint indicates the div into which the application will be displayed.-->
<!--If no mountPoint is given, the application will render in the fullScreen mode-->

<!--jwt will be the JWT obtained by the integrator in order to initialize the session of the user-->
<!--to obtain the JWT the integrator will have to previously authenticate the user against meetingDoctors.this can be done from a server2server call, or enabling new registers from the client.-->


#### `- Universal Module Declaration`
If you download the package via a Package Manager like NPM, you can then require the module into your own JS

```javascript
// ES6
import meetingDoctors from "MeetingDoctors"

// ES5
var meetingDoctors = require("MeetingDoctors")
```
Then you can call any method on the library like
```
meetingDoctors.initialize({...args});
...
```
See below the definition of those args


## `Library API`

### Args
Args will be an object with the following defined keys, this object will be interpreted in the Initialize method and will trigger the execution of the SDK

#### containerId
containerId 'string' : indicates the Id of the doom element in which you want to render the app. If no contaierId is provided, the application will be rendered in FullScreen mode

#### JWT
jwt 'string' : is the JWT provided by meetingDoctors af a particular user.
Using this JWT the whole library will authenticate as said user
There are many ways to obtain the WJT, depending on the integration strategy.

### Methods

#### `initialize({ jwt , containerId })`

The initialize function will trigger the Render of the meetingDoctors app
This method will internally call the two following ones

#### `authenticate(jwt)`

The authenticate function will take a jwt and use it to initialize against all the services of meetingDoctors. This way, the SDK can connect with the notifications and chat service.

#### `mount(containerId)`

Once you have authenticated the widget, you can render it inside any element of your DOM that has a given width and height, and an Id(unique) to reference it.
Depending on the dimensions of said element, the widged will be rendered as partial views or full view.



## `Styles`

The SDK provides some of the styles for a proper render of the Chat, but it is just a default styling of the chat.

The integrator can also add an upper layer of CSS to override the styles and customize to deliver the same look & feel than the rest of the page.

An initial template of the customizable CSS classes will be provided a customization classes below:

```css

/* Widget */
#floatingButton {
    background-color: #38B4E4;
}
#floatingButton.open {
    background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAJAAAABkCAYAAABpRbm3AAAABmJLR0QA/wD/AP+gvaeTAAAACXBIWXMAAA3XAAAN1wFCKJt4AAAAB3RJTUUH4wYUCB8NscfVfwAAGklJREFUeNrtnXmQHFd9x7+/7tndmd3V3mvJtixbsQU6MD7whSzJlrTS6sAchVHAMTi2ZAShgFQRKEPsQgkpbBwSkkASHAwB7HDIoRxAlnVYWnQ5BMscBcY2sqzDspAlrfaes/v98sfszLx+/bqnZ7ZnZyXtq5oqqXemu+e9z/v9vr/f+70ewmSbbHLbzHVoiM8FjLkgvAnADAAXAZgOIIKF0dkg4tzbI5M9dp63Hm5EJHUTBC8A4WYguQAwoh7vfkyGZxKg87XtSs4CifcA9C4geSMYJijA5wjPqIcmATpf2u6hTsD8MwB/DvBVCESMozFYbJ8E6LwDJ7EUTB8DeDWA2jGc6XdY1PDHSYDOh/YC1+JM4l1g+isAN8ApW8prRNt0hycBOtciqCmp9ehN3gfQhaGem7F9EqBztTEb2Jt4Lzj5EBh/UoErJFFft2cSoHNS44y8G3uSDwM0q4JX2YfrKD4J0LnU9iUvh83/DGD1OJi4bV5/mQTobGs9HIWZ/Bxs/jSA6Di5yO2e2npyRM6itjc1D8L+HkBvHcernsTC6DQ1A51rxuSonCVtV+JDZNu/AOOt4HG98jYveCZd2NnQtp9pptrodwF+Z8FlMHIQMaiyfoSwze/PkwBNbKszk1hsAvNceIBClYWJkbInAaqwwCTsTc0CxFUAgIX1T4QDT3y+weJJABfkxpJZkq5FYQJAY6WJfomuxjcmAQqzPcsxiNStsPlGEG7EnuQNANpGR/QpAGMGyOwZej8L/jaAOjnUIckwOGDShEOUhXuMMPHWYu+YBChI28/1SKSWgvl9sJLvBjBF7yp4RxjwAPQYwIWxYXLFzQ6YCpSEC5PAlkmAxuKa9qSWg8XHEE8uz1sD/+EfE0DmzuE7wPguAFMeY5bDrrBh8tZNg2iM/nwSoFJbtkLvDuxJfgLAvBJM/0ksrP1t2fDsGLwb4EfzqRUJFJJAcMLkBqVkmLxEONEzuI4ykwCVAo6Z/AyQ/AQYzWWcYadfvsQfnpGVBPEfYBgFbtg51KyDSXofK4SQEybJ8AQT4Uxbg9z7JEDMBvYm7wQnHwJQfgkEu8s9g7SaHf3XMuyNAEUAOEp3yoYpiKsrAhMsngSoaNud7Mae5D8CmBvC2XaW/Ikd8YuZrR8DaHQXfVHZMJWsm1wRHf8eS+uPTALkF4pnEg8B/HGEk3o7iFtih0p0mdEae+gpZLfLSIOYV7qeMBWY0B6EGmiVKsKJeWtQX3z+AbQnfiOs5GOgEOtnGCVHXzXW4FdAuEpCxCGO2QemQK5uDCLcIGwRAb/H+bWYuitxH5j2Agi3+MrgkvRP7TP9twP4CHh0EPPhEsvBdfblPOx6Xw6m3MtJBztFdu59UAU2Z01g9p8Jq6ZhDyYtkMNdRGAmvwrgIxU4uw0zE9gCRbf2zxSMRynrLAqGQB180timMCxTERHOwC7Mp8S5AdCu+CUA5oNwEUAdiKT/AfObz5QRnv8QwKoK3eX+Uu7JJnyD8mkCloIgcg4162CScGKFOQoNpi2l5CImFkAvcC160ysBcTuARcjuy861E3h70/2lieWBNmRSOwBcXcG73hbc+vTdJYClUD1NYJicVMi6idkLpqAiPAuTgNiCsw6g3SMXgoxPoDf5YQBtHkJ1c0mJuq3cACv5ExBfXdF7F9ge6H1bBtoY4mHKjTSRuy6sIjAFdXUMgA5jSdPLZw9A+4YugB3ZAOAecJG1JuLNJYXpVnITgJsr/A2GgqwXAUCtIb4MzpVmZEeZpJjbF6Z8WF46TKXoJqZgycPqA/QC16I3+SnYuA9AU4BPpFEbCzbTmQ3sSXwfoFsr/0W4J8h6Ue1TZ640BN9ViJxJvWdZM4N1qSnWwxSqCBe8ZeIDtCt1JXpT3wFwTSnZG9xEg4HeuTf5QPapE+PQ2Aikf0wSX2Q2jLxbknwMu2AaXZOSlC37wFSaCPeFKWOz1TNxAdrIJqYlPweIBwDUlPTZoO7rZ8llYH5gHKdDUYDqnz59PTOtzi1UspK1IxkmdV2K80eLwBRKRLcPy9oGJiZAe/pbwcnvAVhR1ufJeKq45UnMIFv8EAwznHLOou0QbokeKO5R8RDAlIujSRIdrGSCfeubZZgqIMIRcPVdbZXPRO9Nvhmoe7ZseIDDWBB9ucgoEQk8AqA112XEnH9VZBsMFbc+jZvOvIUYS7JZYh61H6xkhbPHqZAJRs7W+N6/9P30xZG5F49qLFYy0HAkq4ntLeV0Q2Ut0O74zRC8OaBQ9gyAi86C3fEPM+cAdRdPuYrNw9i94LNbszCp7buJc2EySR6ECzk8xwIoSy7FyzKFK8JH8+En0stafjOxLNCuxCKAnh4jPAAMf4B64tPBeDi/djQ6o3MzT5295JrdZZknG5T2L9/o4QgYd+Q8Rf56EgmyZSLJMsHXMinWVQNKwTJ5fDfFMoGxtdxiuMpYoJ8lFoPwFIDYGM+UgVG7038GiIfAaPKtxnNwROpbnVFRMP30Cyxs6fMVz8OnlhMwTT0nSZZAtkx5S0l5r+xhmZzfgUKJ6LC13AEKH6BdqTkg/hHAsRDOtg8LaMjrjzU74zcKFnfkchpOoegNlN+WGDdQGnfHxfWPwXxnXsYStIXsDphyb5RhyvElfZ+8CB9LROcU4SJdQ9snBkA9w9NA4umcmB17nsV/ZgjYX872tdy5Eig6oEqsFdbrpyL6Z+MLtcRYrYu2iFSrSNDnh4rrJnKkkf10k24S5EX1fixuOl22wAgvqcYGTPMxAJeGds6Id2QQeWZoMTEWuMIJZo/aF/nvGl0haSN//SQGUR/7hd9tN9d13AJwky7actyf7ppShF1MNyGwbvKJ6Lh89xWuBdqb/CyArhDt2QnMb/CODEj8NWAUX2WWZ6v0Dw64m8Ht7mhHseULFvzOnKXJSxnPPNBoSo8KloElN+Onm8KI6MgMXk1QOYD2DV8NGxtCdYfs/ViRmh0DNzDT0qJlC6SUcHoC5a2fSKmjERxk9Z3f4b4feaClPDC5QZVhCirCSck0BxHhBAwmWlv/b0wxchiuiyzj38ActiDf6pPdvZ8glXFqy0JZMvlwDqTyHtXdkYdLzAbwpu+MbXny2NUEXJZzNWCP+1HOT5JLU12oHLp7ujlWS1elUJ41yUtmMPOOIIvBlbVAe+IfBujtZYbD3vqYLO1Mr90+NIdZvEOebeSsy5RcQIk7G4oVojMdxNLoQf8JZb6zcM5Ra8LKeSh7LYerJMUyjd6/6kI9IzqXxSru6kyUH32FA9BWbjBE/PMsdZgjMi4fqOexaMopD4HxASKHJXeqYXiVfbISieiAKuLuglQfMt+md00AETlCanmgZQsp6yZSJoN/RJc9SErm2cvV2bC2VRUgoyb+STCmyR3mlbQrCSjyiwz4drD8UV1hOispHg1QgTbyqWEY+yY1O350+EIb/DZntQVJusRBk2Ogg8CkF+Hk1GrBRfjB1OqpB6sH0GauIxr5uHPwyC08AwMlhT+sL2yq2dZ3NYA50FgfV8WeR4EVwZn99QKKmFRjxLZNvttdLFGzgoiJpIsxeBxhCh7RMXgrQmhlA2TWDX0ITNNcPts5KiUAlf9DP4uYNjIwGe8t6AhyMeLIzQYGKuAuh4x9Et0tvk/rMoi7wZIrZOn8PjCpAx0EpjFHdGxsDwOg8qIwZiLQXxK7k3ikRhSa5J1v4o7xDBaTpY/spa05jnIGzfqzq5RBKWeQyx1G/yO/xxHdMQMjI6/4Z5/ZBHMXwErkp+8btV/yfab0B0nRFuSozhFhaiI61kR0hWtYUZN2Vs0CmTsHVwA0V2/qnQk6bb7Fx0IRY6utuWbDUyen2czX6F2eus6jlDRo3Z1koYq5OwA0mDxg+/RJu3HsOgi0syLq5f7h3LlZ2UWh67MiIpyVRdIgIlyyWM+dWdU+WDWADBh3FsyuUibp2LzvTtAVA8o29JVxtmmuJGbiPHROn6MC5XBwWndXmn7ik30H/bPP6M4Xd3kMNDm0lwSqrs+K6KaxRHRECMX6lAdQD0dhDb7DUTLpEKSsDCTpw2QNUAQ+IG5peE2/coGVea3kyK14AOV4PIXi4krUTxxPQQwODfl1Cwl05xfTPQY6CExBddNYRLhgsaNqANVaA6sBamJNDqYYUJ7urrBms8cD2gjFe5flT+8obygA5SyV8CttKFLBp1bvDQz59lXLk4daKCVuKHxVkkRuqTDBscJeAZiSQ2nr59WzQOD35DuKdDrCDygfdweADaEFqDF+aj4ztbAjg+uul5FrZXytk6+7c+sn0TcMMJtePVKTNLpyfclSPoyUSJMDweTMiFcgotuHNZckqgPQRjbB/SsCmX4voJj07g5AjS12a4WqjW4YUNPP0AIlg1OWu3PrJwwM+/cVc3dBNCt6ipSBzkPPyrIJSVa0DBEuh+755RJ2pEyyyyAUmvsqGaBoU998ZmqHl0ANCpTsUXJApTN2clX7q1p9QVjmXP8ZnV0eFX3e1XwadwcnMGqGnBMpcCoNkOFpgYh5uQsA3YRxWBO9q5NFOLs2EJYqwt0RHRu0s2oAAVhN+YGkPOWeAtULKN0a1cCI1qw2b+pvFSJ1rWN+aRYU5UVGT+ukujsNUOp5RNb6AKTvqwt/cHiObfOMPACu7yjDJE0oD1fnBVNwEe6d2CVQ/0Dz1OerBpDBfFsu5aaWZ+fdQBlAMQM8OKyNcmwrsZSIzIL5d5aDunWP2zoFBkqjnzgHEFibdBW2vYKYtFaDpEFVl0yoRJjCiOhAvM0rSVtxgKI/6Z8JtuZCBw8oG/VQeUARABoY1G6rJVBXHoYgFsSlhwIClT+P091x/4hvXxFTt9tqFCZGvofGDSZvEc6CtiDkFhigiGmtEgw9PEGO+QGVscDDiWEPq9eV71/FgrhraGTI3C7JVz+peogAkcqAU6ncfbs00GX/eSiaZLHQtdNBt6fdAyZVHwWByR3R6d2moo/YrLW3Vg0gFmIFkbqfgUIBCgPDgICrMq75JydmwhKXk3PNIi8lCp3jBErv7krXT5L10fZVmngRGPWQoh65JK0AuLKdRpcJ10Sn/hGdZJ1c0kAb0f3m9LtmHK8OQJsP1JGFW+VbIjk+9gAq6DE7qzPcvjkjlpEOBCJnwZQXUFDD59L0k+iXjSLVuyYVcTdBX7yeW1R1wORKYjotVkVFuOCnUYEWCKDmTNMiAW4swONO3OqACnoMgyMQ7AbIALrkBUXZgjiKLSSgHFu8JKBKdncMiMEh2Sp1uPWZ6PYqXs87wxJg0otw0hbClaqbjADPGKgYQDn3xbLpLGKNAh+zGSIbwTsB2sAG8PpiZ9LMUTxb0ASsHFeBCuLuFKvF8RQ4bUlaDB1ykvPixw9MZwvzvLYjI7fsWwJMfnmgMYrw/lP9J/+3agCB0S3HJ054PKyRFJX5ASWGRoCsOnckoTve8tq1QhgdDnAUXSAXnXsCFdTdKUDl8z+FdzksEFvoJnC2V4rsbQ8Kk94FjV2EM+N/sP66TFUAavvRsek2eF7hW6vwjM0aSQNlOa0edZFscUgOT1kacC+gPPRQEKAor8vkNlXJPnerUZsXTKrV8ILJ+TS6YBGdX8Y7BxOx8UNUqBWtSLRhrKJ8NV2hgtD7GCvH4HtMEqqqBuqC9AAlkioMAfn6kKr02KNKjz0q/lhb8ceWBXs4rnZFBzb8tD63JkjMSx2PV2HNY1ekisZ85aRS6ejadsySPpL6uXA+5cFSugdJOfbL8elTQ2/sqBRARS2QKXiFvEPB2/KUbo3YtiHiydyUM+T8yrAQ8wthquM5FFJoy3rrVK67Gz2Z1TecdatqsxouAfDyxQMvXg/TbAPgekYP54vXNeuFLmvivYM0RBH+ZKXcV3GAHtlfA/AScuRSCqAUP+Yfqdn9w1IYxPkHUcVj5iJijuVWmR3gqEBpIjAtUPBzd06gMn362rGakfhNGeBlwzCWIQA42uSpj6urhAgnwg9Qwebrwjpap84n5mbVnLpdlv8xMIOEsg2XGfZgXEYj/zOTQoguQD0XJDeld0nk4ZIIetdGjkL3nPuyYQ+N6EJRIDm0FAAMkXVf5Nhm7H5qmPZJYroniMnbkTVPKwNkVwdHSa7LzQFyf5x4I3LprkoC5GuBSGBFoQrZaWVKPwaXu1OEakuBau5yzDxtZlapp1GskzsrK9fYKOeRIjBrQO++KJ0CC3vWRY/sr2fCTTIkQayQ3jKFK8KdO5EITPhvrCG7agAxeGXhi48FHvUYwY4nINKSaxbcAgDTNh7o5AyuYih6gXW6Rw5Zg7g7r/MU3F3aw30hnQbbuNikhoXw+AnwSsHkuRibO+6YbIVlFWb+PircPAHq3HhoGmzx1vDhGdWj/cpAJeNNuLUnwunIEoANhziULIgWBIIzn+IFFNTzOPWTyFiwhuJ6a5xJAiLTDiPYM5DKgSl/XFm0ZlJgKpofAgTRr09+8IpnqwYQLKzMSrSw4ckes5Q8C2WSJt50+lLwpUtyOW8mRRw6FiPdlsjt7mQzr0n1K+4u3Tvg/dTWdApkWTFSf64pRJgCQRYwojMZX8U4NE+ADMErnJnk8OCx0xnYibSiMdIwjcgcYl6S9/XOvcZ5oEhZkXK7O+V4AHfHzEifGfR05pRJg+rqBFD4ndNyWmArNKaIjg63xpKPH68aQBvZpOSrXTDyyfpQdZA2TE6nUNPRfj0xX+GM9gsWpChQJGsEH/0Et7vLDAxBWLaH+8oAQqCuo7MXkH6yaYytFHBK0U1E2PDCmnnpqlmgqelXrgeMNnW2u3M8pB0U32MMt1BlBllpRJta5sui3W1BfICSXFs5+inZ67PTN5MtKqvvbD8TJkAVEuHPvX74iscwTk1fpimM5a7Z4SoKU61TsGPWSAJ2OqPM8OxkqWmMzYDOv8u1NgpQjuMa6xREP2XiKViJlPfAprP3V9vYMGW8BqZMmGw2aD02kKgqQIYQy/3h0a3EBwMq2aepXE1nlzNqmhpbnYKxIAwdT1xnr71f5bm7+Mk+/17KJGE2NGbIMC5GFVoJIvyLx++a9avxvDcXQG2PH2iiDN/gD0951ohtRnowrtEYaZixGBtkdOYLujThrDdQJbo7yT1aIwlk8utx8IzAopfMOAmgKgAFhOm5qZmhL7w+zvfjAqg+JZaCsj8IF7i+OaA1ivcNgllos7y1nRecIeb2XMcEyY+4dI9vBKYBikkMn+z3r0gQAmRZiLW3DU4EgDxg6oVhvv/5Ci6aBgaIwMu9f+SlfGskWCDRN+wpUus72waIud0LHj1Qqsgnd7LNRz+N9A0KK5X2BYgyKcAgRBpiF2BiNouI3nfknje9Wo2LuwFisSzoj2mVYo1SA8MQlmZPm7ABYaOmobHFK7Qt61gR/cRC9I30Dhb/TY90EpHm1gSB2icgPEyg9UfWzu6p1g04AJr+6AtXAHS5V56idKBGw3fBGDkz4KkvIg0NNhnUFjRXEkhU+usn0X/8dJJF8WCFMmlEp019A8BlE5Cf+46sm/Otat6B4bQVtLyYzy3llSuZiPcPwraEp4uo67gg8K/FqCUSrmt6HHOUUQh+MJVI9Qe6YDqFWFtbcsJZHqLPHF039+Fq34gCEJaXKuKKvey0ZQ17aZ9RAR3taBsuV0SWDJTgLa83zvo8QIHWigzbQiRae8kEgscGYf2RtbP/fiLcTB6gtz2yvwagxWONCpSXGBkY/Bb7ucJUmmtj9R1hRSVFgPpdtM74U6whW0SGvgOg1/d8Vhq1re2DABomCDxpgD5wdO2cb0wUmvMAnTRiN2HMv2/qiuj+dih+5tMAPH+PvCZWl4ZBzZUKc6XXKwC6X7lzVnbNYsNtcQBfL+a+6jraT02IkB04RUwrj66b/cRE8qUFF2aYy0J10uCnj742+wvYsGoQRN/0muHRzo7ecfiehy3DWvLa2tmOBWqRrvkSgBO+7rW1RVQdHsYuu8a45si9s3digjVDCt+7Qzzv/mSK1+TWZITJXwHcD09AKo1Ye1u8wlP3pYgtbjl+z5Xup78+vGCIiD/v2TnMGbMmUs3oi0H4lw4xsuzYXW9+HROwGaPhextAbwvpnL+vydSsPvWxeQVhvGHxMYCecFuglB2JVTBBR3guTZFFr66fd9RTkb50+psE0v6EZW1TYy+QzcpXob1KTF1H1875ZDUyzCUBZJDZBcAMYcK8SDZ3HfzoFSfVvwiiL0N5hHdtLHoqbN0l3cvjljVy64l7ZvlrmCfW2LbNdwFwhupCINbSNlgFm5MA428MMzpvIrosvQtjhKF/egR4wZH1c/+o/esXbvkVAz+WD8WamyoxQEkm+ujRdXM/eHz9dcHc44OLXwLwd04BnUS0eUrtOCvlTUYEc4/eO2fD4btnJnEWNGNU8C4fy5xhwr922iPdx9bNO+P7RoEHshussv+JtkwxQh6AZ4nNa19bO/vrpX5URPAlAvIPoIwQDVDEuHQcxkAA+CmzWHR07ZzbDt895zDOokaXPfLybGGKF8v8/AliXnvk3rmbAxN7/8/+C+A7jEwyfdEVM20Qx0L4HscB/O3RY7O/MaZiqs/2zDZMeh7g+ilR87fN0zqvrGDfpwDaCMN+6Og9836Ps7RFhMnlRF8jAH0tYtc8+Or6ywdKm+n8KcPCqrpo9ASIZ4+R/9eY+J94SuO/Hwvj6esPLn4J9/d8BsDXYk2NlakpZvySCN9PGZHvFNVnZ4MFmvHoi5sArA4qkpnoUdsyvnt8/ZtPl3tR44Gdf9He2nRHrKnh5jJuuR/g7cT87SPNc7aGv/OSie7v2TT90mnXENGFIZywj8E/Jza2CLI3H1s37xWcQy0C0O8A0QxQJwitYIxkoyVOMXDYgHEIJH4JYew8cu+cQ6E4fXP3182629sBGgDETIA6kd3aLFcH9AI4DdAxsDjAhD+wwc8ea5y7v7LbdYljYv86ImMNg6eDqZUMboZACwityO7hl7VbEkCCGMMMfgOEPxIZrwuBP0RI/PrQurlHcA63/wcgFqrHKtJZAwAAAABJRU5ErkJggg==);
}
#floatingButton.close:before {
    color: #01a8e7;
}

/* CloseButton on Widget Fullscreen */
.closeButton {
    color: #CC6666;
}

/* Headers */
#meetingDoctors .contactList .meetingDoctorsHeader {
    background-color: white;
}
#meetingDoctors .roomHeader .meetingDoctorsHeader {
    background-color: #01a8e7;
}
#meetingDoctors .professionalDetail .meetingDoctorsHeader {
    background-color: #01a8e7;
}
#meetingDoctors .meetingDoctorsHeader .logo {
    background-image: url("https://www.meetingdoctors.com/img/logo.svg");
}

/* RoomHeader*/
#meetingDoctors .roomHeader .professional_name {
    color: white;
}
#meetingDoctors .roomHeader .professional_speciality {
    color: white;
}

/* ProfessionalTile */
#meetingDoctors .professionalTile {
    background-color: #e6e6e6;
}
#meetingDoctors .professionalTile.active {
    background-color: #c7c7c7;
}
#meetingDoctors .professionalTile .professional_name {
    color: black;
}
#meetingDoctors .professionalTile .professional_speciality {
    color: #01a8e7;
}
#meetingDoctors .professionalTile .professional_schedule {
    color: gray;
}
#meetingDoctors .professionalTile .roomMessage_lastMessage {
    color: gray;
}
#meetingDoctors .professionalTile .roomMessage_pendingMessages {
    color: white;
}

/* Room */
#meetingDoctors .room .roomOutput {
    background-image: url("https://meetingdoctorsgroups-userfiles-mobilehub-300209103.s3.eu-central-1.amazonaws.com/protected/Room.Output.Background.png");
}
#meetingDoctors .room .separatorBubble  {
    color: white;
    background-color: #01a8e7;
}
#meetingDoctors .room .dialogBubble--self  {
    background-color: #EAEAEA;
}
#meetingDoctors .room .dialogBubble--contact  {
    background-color: #e3f2fd;
}
#meetingDoctors .room .dialogBubble--self .dialogBubble_content {
    color: #2d2d2d;
}
#meetingDoctors .room .dialogBubble--contact .dialogBubble_content {
    color: #2d2d2d;
}

/* Detail */
#meetingDoctors .professionalDetail .professional_name {
    color: black;
}
#meetingDoctors .professionalDetail .professional_speciality {
    color: #01a8e7;
}
#meetingDoctors .professionalDetail .professional_schedules {
    background-color: #01a8e7;
}
#meetingDoctors .professionalDetail .professional_description {
    background-color: #01a8e7;
}

/* Scroll */
::-webkit-scrollbar-thumb {
    background-color: #01a8e7;
}

/* No speciality icons */
#meetingDoctors .professional_icon {
    display: none;
}

```


