### Module 04:
- #### Variable scope
    - Scope essentially means where these variables are available for use. 
    - Different Scopes
        - Javascript has 3 different scopes : Global Scope, Function Scope and Block Scope
            - Block Scope
                ```js
                    //Block Scope is set just with {}
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
                        //All these variables are declared and works on the function scope.
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
        - Redeclared: var variables can be re-declared and updated. For example
        ```js
            var a=5;
            var a=6; // no error triggered. var can be redeclared.
        ```

        - Scope: var can have functional scope and global scope.
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
        ```
        - Hoisting: Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their scope before code execution. This means that if we do this:
        ```js
            console.log (greeter);
            var greeter = "say hello";
        ```
        - it is interpreted like this
        ```js
            var greeter;
            console.log(greeter); // greeter is undefined
            greeter = "say hello"
        ```

    - let
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
        - let can be updated but not redefined, for example
        ```js
            let a="original value";
            a="new value"; // no error, a can be updated :)

            let a="new declaration" // error: Identifier 'greeting' has already been declared
        ```
        - Please note that if the variable is defined in different scope there will be no error.
        ```js
            let a="original value";
            if (true){
                let a="new value inside of a new block scope";
                console.log(a) //new value inside of a new block scope
            }
            console.log(a) //original value
            //no errors :)
        ```
        - Hoisting: Just like  var, let declarations are hoisted to the top. Unlike var which is initialized as undefined, the let keyword is not initialized. So if you try to use a let variable before declaration, you will get a Reference Error.
    - const
        - const can have functional scope, global scope and block scope
        ```js
            function foo(){
                {
                    const c=3;
                }
                //c is not accessible outside of the block
                console.log(c); //undefined
                const c=3;
                console.log(c); //3
            }
            //Out of the function the variables c is undefined as well.
        ```
        - const cannot be updated or re declared
        ```js
            const pi=3.14;
            pi=3.14159 // error: Assignment to constant variable. 
            const pi = 3;// error: Identifier 'pi' has already been declared
        ```
        - hoisting: Just like let, const declarations are hoisted to the top but are not initialized.


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
    - A closure is created when you declare a function within another function. The inner function has access to the outer functions variables and parameters. If you expose the inner function, then you can access the outer functions variable and parameters in a controlled way, through inner function. 

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
    ```
    - In the example showed above, the function Addteam is able to access teams (not declared directly into it) and modify it.
- #### Hidden variables
    - When an object is set, many of their properties are visible and can be modified at any time. For example:
    ```js
        let chivas={
            campeonatos:12,
            numeroUpdates:0,
            addCampeonato(x=1)  {this.campeonatos=this.campeonatos+x; this.numeroUpdates++;},
            getCampeonatos(){ return this.campeonatos;},
            getUpdates(){ return this.numeroUpdates;}
        }

        chivas.addCampeonato(1);
        console.log(chivas.getCampeonatos()); //13
        console.log(chivas.getUpdates()); //1

        chivas.campeonatos++;
        console.log(chivas.getCampeonatos()); //14
        //There is still one update because campeonatos was accessed directly
        console.log(chivas.getUpdates()); //1
    ```
    - In the example showed above, update was not increased when the variable was accessed directly. There are some ways to hidde or to prevent a variable to be accessed directly. Using Closure for example:
    ```js
        function chivas(){
            let campeonatos=12;
            let numeroUpdates=0;
            function addCampeonato(x=1){
                campeonatos=campeonatos+x; 
                numeroUpdates++;
            }
            function getCampeonatos(){
                return campeonatos;
            }
            function getUpdates(){
                return numeroUpdates;
            }

            return {addCampeonato, getCampeonatos, getUpdates}
        }

        let ch=chivas();
        ch.addCampeonato(1);
        console.log(ch.getCampeonatos()); //13
        console.log(ch.getUpdates()); //1
        console.log(ch.campeonatos); //undefined
    ```
    - Now, only the function are available and the variables are hidden into the function itself.
    
- #### Lexical environment
    - Variables in JavaScript are lexically scoped, so the static structure of a program determines the scope of a variable (it is not influenced by, say, where a function is called from).
    - Each time a curly bracket ({}) is created, a new lexical environment is created as well. It is used during the compilation to get what values should be taken for each variable. For example:
    ```js
        let bar="im a global variable";
        let global="global"
        function foo(){
            let bar="im a function variable";
            {
                let bar="im a block variable";
                //This time JS engine try to find bar on the block, then on the function and at the end on the global scope. Since it was found on the block first, then does not try again on the other scopes.
                console.log(bar); //im a block variable
                //This variable instead, it will be not found on the block, then will look at the function and then will find it on the global scope 
                console.log(global); //global
            }
            //JS engine try to find bar first on the function and then on the global scope.
            console.log(bar); //im a function variable
        }
        //JS engine only find the variable on the global scope.
        console.log(bar); //im a global variable
        foo();
    ```
    - JS engine look up at the first block where it was called and so on until find the variable assigned. 
- #### Nested functions
    - A function is called nested when its created inside another function. For example:
    ```js
        function foo(countryFilter){
            let countries=["Mexico", "US", "Germany", "Japan"];
            //filter function is called inside foo function
            function filter(name){
                return countries.filter((country)=>country!==name);;
            }

            return filter(countryFilter);
        }

        console.log(foo("Mexico"));
    ```
    - Here the nested function filter() is made for convenience. It can access the outer variables and so can return the list filtered
- #### Code blocks
    - Javascript statements can be grouped togheter using codeblocks, that is, set the code inside of curly brackets ({...}). 
    - Each time a code block is created, it creates a new lexical scope. New variables will be available on the block, but not outside of that.
    ```js
        let a="defining a";
        {
            let a="redifining a";
            console.log(a);// redifining a
        }
        console.log(a); //defining a
    ```
- #### Overriding outer variables
    - Overriding outer variables or shadowing, is used when you need to maintain two or more variables of the same name. In that you must use separate scopes. For example:
    ```js
    var studentName="Suzy";

    function printStudent(studentName){
        //Altough studentName is Suzy on the global scope, it is getting shadowed or overrided 
        //by the declaration of studentName inside of the function
        studentName=studentName.toUpperCase();
        console.log(studentName);
    }

    printStudent("Frank"); //FRANK
    printStudent(studentName); //SUZY
    console.log(studentName); //Suzy
    //studentName, global scope was not modified by the assignation 
    //studentName=studentName.toUpperCase();
    //because the one that changed was studentName on the function scope.
    ```

    - Since the lexical scope is different, studentName inside function is the one that has been changed and not the one from the global scope.


