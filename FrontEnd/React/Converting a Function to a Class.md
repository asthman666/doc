## Converting a Function to a Class

    function Clock(props) {
        return (
            <div>
            <h1>Hello, world!</h1>
            <h2>It is {props.date.toLocaleTimeString()}.</h2>
            </div>
        );
    }

You can convert a function component like Clock to a class in five steps:

1. Create an ES6 class, with the same name, that extends React.Component.
```diff
+   class Clock extends React.Component {
        function Clock(props) {
            return (
                <div>
                <h1>Hello, world!</h1>
                <h2>It is {props.date.toLocaleTimeString()}.</h2>
                </div>
            );
        }  
+    }      
```
2. Add a single empty method to it called render().
```diff   
   class Clock extends React.Component {
+       render() {

+       };       
        function Clock(props) {
            return (
                <div>
                <h1>Hello, world!</h1>
                <h2>It is {props.date.toLocaleTimeString()}.</h2>
                </div>
            );
        }  
    }           
```

3. Move the body of the function into the render() method.
```diff
    class Clock extends React.Component {
       render() {
+           return (
+             <div>
+             <h1>Hello, world!</h1>
+             <h2>It is {props.date.toLocaleTimeString()}.</h2>
+             </div>
+           )           
       };
    function Clock(props) {
-        return (
-            <div>
-            <h1>Hello, world!</h1>
-            <h2>It is {props.date.toLocaleTimeString()}.</h2>
-            </div>
-        );
    }    
}    
```   

4. Replace props with this.props in the render() body.
```diff
    class Clock extends React.Component {
        render(
            return (
                <div>
                <h1>Hello, world!</h1>
+                    <h2>It is {this.props.date.toLocaleTimeString()}.</h2>
-                    <h2>It is {props.date.toLocaleTimeString()}.</h2>
                </div>
            );                
        )
        function Clock(props) {
            
        }
    }   
```
5. Delete the remaining empty function declaration.    
```diff
    class Clock extends React.Component {
        render(
            return (
                <div>
                <h1>Hello, world!</h1>
                <h2>It is {this.props.date.toLocaleTimeString()}.</h2>
                </div>
            );                
        )
-        function Clock(props) {
            
-        }
    }   
```