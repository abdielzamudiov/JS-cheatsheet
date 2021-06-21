### Module 04:
- #### Variable scope
    - Different Scopes
        - Javascript has 3 different scopes : Global Scope, Function Scope and Block Scope
            - Block Scope
                ```js
                    //Block Scope is set with {}
                    {
                        var a=2;
                        let b=2;
                    }
                    // var variables cannot have Block scope but let variables can.
                    // a is accessible here but not b.
            - Function Scope:
                ```js
                    //var, let and const have functional scope
                    function foo(){
                        var a=2;
                        let b=3;
                        const c=4;
                    }
                    // a, b and c are not accesible outside of the function
                ```
            - Global Javascript Variable:
                ```js
                    //A variable declared outside any block become Global
                    var a=2;
                    let b=3;
                    const c=4;
                ```
- #### var, const, let
    - var
        - var can have functional scope and global scope.
        ```js
            function foo(){
                {
                    var a=2;
                }
                //a is still accessible here
                console.log(a); //2
            }
            //a is not accesible outside of the function
            console.log(a); //undefined
    - let - const
        - let can have functional scope, global scope and block scope.
        ```js
            function foo(){
                {
                    let b=2;
                    const c=3;
                }
                //b and c are not accessible outside of the block
                console.log(b, c); //undefined
                let b=2;
                const c=3;
                //The variables a and c can be declared out of the block
                console.log(b, c); 
            }
            //Out of the function the variables b and c are undefined as well.
        ```
- #### Hoisting
    - var
        - A variable "var" can be used before it has been declared.
        ```js
            //using var before to declare it.
            b=2;
            console.log(b)//2
            var b;
        ```
        Hoisting is JavaScript's default behavior of moving all declarations to the top of the current scope
    - let, const
        - let and const are hoisting as well but not initialized until the variable is declared. (The time between the start and the variable declaration is known as Tempral Dead Zone, the variable exist but cannot be used.)
        ```js
            b=2;
            c=3
            console.log(b);//Reference error
            console.log(c);
            let b;
            const c;
        ```
    - Only declarations are hoisted
        - Javascript only hoisted the declaration and not the initialization, if you want to use hoisted you will need to initialize the variable before to use it.
        ```js
            console.log(a); //undefined
            var a=5;
        ```

- #### Closures
    - Function can take local or global variables to work on. For example:
    ```js
        //foo can take a global variable like a
        let a =2;
        function foo(){
            a++;
            console.log(a);
        }
        //or can create one inside of the fuction istead.
        function foo(){
            let b=2;
            console.log(b);
        }
    ```
    - Closure is way in that the function has access from outer scope even while runnning in a scope where those variables wouldn't be accessible. So the function create link to a variable and that link is available as long as the function is live.

    ```js
        function foo(){
            let teams=["cruz azul", "america", "pumas"];

            return function Addteam (newTeam){
                teams.push(newTeam);
                return teams;
            }
        }
        //b now is refearing to the function Addteam
        let b=foo();
        //Altough Addteam does not declare directly "teams" it has still access into it
        console.log(b("chivas")); //[ 'cruz azul', 'america', 'pumas', 'chivas' ]
        console.log(b("tigres")); //[ 'cruz azul', 'america', 'pumas', 'chivas', 'tigres' ]
        //each time foo is called, it create a new reference to a new variable "teams"
        let another=foo();
        console.log(another("real madrid")); // [ 'cruz azul', 'america', 'pumas', 'real madrid' ]
        console.log(another("barcelona")); // [ 'cruz azul', 'america', 'pumas', 'real madrid', 'barcelona' ]
- #### Hidden variables
- #### Lexical environment
- #### Nested functions
- #### Code blocks
- #### Overriding outer variables

