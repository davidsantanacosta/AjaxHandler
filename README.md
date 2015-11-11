# AjaxHandler
AjaxHandler for simplemvc framework

Include it like this in your controller

``` use Helpers\AjaxHandler as Ajax; ```

You can do ajax requests GET/POST with Jquery

```
     $.ajax({
            method: "GET",
            url: "mycontroller/myfunction",
            data: {mystatus: "allok",yourstatus:"allgreen"}
        }).done(function (res) {
           
            if(res.success){
                console.log(res.message);
            }else{
                console.log(res.error);
            }
        });

```

Then in the controller you can use it this way, no need to check if is a post
or get request, the get method can "get" both requests

```
function myfunction() {
        $mytest = Ajax::get("mystatus");
        $yourstatus = Ajax::get("yourstatus");
        if ($mytest) {
            Ajax::success("Received");
        } else {
            Ajax::error("Houston we have a problem");
        }

    }
```

And the json generated by the class should be something like this if sucessfully received
```
{"message":"Received","success":true,"duration":"0.0001"}
```

You cannot do 2 or more consecutives ajax responses on the same php function
for example

```
if ($mytest) {
        Ajax::success("Received");
        Ajax::success("This second ajax request won't work");
     }
```

When using Ajax::error as a response,  the done function on jquery wont catch the
 response you should use the fail method from ajax

```
 $.ajax({
            method: "GET",
            url: "mycontroller/myfunction",
            data: {mystatus: "allok",yourstatus:"allgreen"}
        }).fail(function (res) {
           
        });
```