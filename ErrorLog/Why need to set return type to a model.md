In C#, sometimes, we design a api return struct like this:

    new {success = true|false, errorCodes = new List<string>()}

We maybe use this struct in somewhere, like Controller/Filter/Model.

In Controller, we write code like:

    var returnResult = new {success = false, errorCodes = new List<string>() {"CODE1"}}
    return resultResult;

In Filter, we write code like:

    var resultResult = new {success = false, errorCode = new List<string>() {"CODE0"}}
    filterContext.Result = new JsonResult() { Data = resultResult, JsonRequestBehavior = JsonRequestBehavior.AllowGet };

We write code `errorCode` by mistake, the correct need to be `errorCodes`.

When font-end use the return data, maybe cause some issues.


So we need to define a class like:

    public class ReturnResult 
    {
        public bool success {get; set;}
        public List<string> errorCodes {get; set;} = new List<string>();
    }

and use this class as the return result struct, we will not make this type of error.    