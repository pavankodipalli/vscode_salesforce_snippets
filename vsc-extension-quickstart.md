# Features

This extension has useful code snippets for the following
* Apex
* Visualforce
* Aura Compoennts (componnet, controller, helper,design)
* Web Components


### Apex Code Snippets
#### Variable declaration
* __vd__ : primitive variable 
primitive datatype variable declaration
<!--code snippet generator 
${1|String,Integer,Date,Boolean,DateTime,Decimal,ID|}   ${1:variableName} = ${3:defaultvalue};
-->
* __c__ : custom object or field
custom object or field
<!--code snippet generator 
  ${1:variableName}__c
-->
* __vs__ : string variaiable declaration
variable with default value
<!--code snippet generator 
  String  ${1:variableName} = "${3:defaultvalue}";
-->

* __vgs__ : variable with get set
variable with getter and setter
<!--code snippet generator 
  ${1|String,Integer,Date,Boolean,DateTime,Decimal,ID|}    ${1:variableName} { get; set; }

-->

* __vl__ : list variable
primitive data type list with default initializer
<!--code snippet generator 
  List<${1|String,Integer,Date,Boolean,DateTime,Decimal,ID|}> listVariable = new List<${1}>();

-->
* __vsl__ : string list variable with 2 default values
string list variable with 2 default values
<!--code snippet generator 
  List<String> ${1:variableName} = new List<String>() { "${2:value1}","${3:value2}" };

-->


* __vo__ : sobject variable declaration for new record
sobject variable declaration for new record
<!--code snippet generator 
  ${1:sObjectorClass}  ${2:variableName} = new ${1:sObjectorClass} () ;

-->
* __vol__ : sobject list variable with default initializer
sobject list variable with default initializer
<!--code snippet generator 
  List<${1:sObjectorClass}>  ${2:listVariableName} = new List<${1:sObjectorClass}> () ;

-->

#### SOQL Statements 

* __soql__ : standard soql statement
standard soql statement
<!--code snippet generator 
  [SELECT ${1:fieldList} 
 FROM ${2:objName} 
 WHERE ${3:condition} ];
-->

* __soql_one_rec__ : soql query to fetch one record to new sobject variable
 soql query to fetch one record to new sobject variable
<!--code snippet generator 
  ${1:objName}  ${2:variable}  = [SELECT ${3:fieldList} 
                                        FROM ${1:objName} 
                                        WHERE ${4:condition} 
                                        LIMIT 1];
-->

* __soql_listvar__ : soql query to fetch more than one record and assign to list
soql query to fetch more than one record and assign to list
<!--code snippet generator 
  List<${1:objName}> ${2:variable}  =  [SELECT ${3:fieldList} 
                                        FROM ${1:objName} 
                                        WHERE ${4:condition} ];

-->

#### for loop

* __for_primitive__ : for loop to loop through primitive list
for loop to loop through primitive list
<!--code snippet generator 
  for (${1|String,Integer,Date,Boolean,DateTime,Decimal|} ${1:variable}): ${2:listVariable}) {
    $0
}
-->

* __for_inline_soql__ : for loop to loop though soql records inline
for loop to loop though soql records inline
<!--code snippet generator 
  for (${1:objName} ${2:variable}: [SELECT ${3:fieldList} 
                                        FROM ${1:objName} 
                                        WHERE ${4:condition} ]) 
    {
        $0
    }
-->

* __for_new_soql__ : for loop for object list with new variables
for loop for object list with new variables
<!--code snippet generator 
  List<${1:objName}>  ${2:listVariableName} = new List<${1:objName}> () ;
${2:listVariableName} = [SELECT ${3:listVariableName} 
                                        FROM ${1:objName} 
                                        WHERE ${4:condition} ];
for (${1:objName} ${5:variable}):${2:listVariableName} ) {
    $0
}
-->

#### control statements

* __if__ : if statement
<!--code snippet generator 
  if( ${1:condition})
{
    $0
}
-->

* __ife__ : if else statement
<!--code snippet generator 
  if( ${1:condition})
{
    $0
}
else
{
    
}
-->
#### exceptions
* __tc__ : try catch with System.debug error flow
<!--code snippet generator 
try
{
  ${1:statements}
}catch(Exception e)
{
    System.debug('The following exception has occurred: ' + e.getMessage())
}

  
-->


#### Debug statements
* __sdv__ : system.debug for a variable
<!--
System.debug(' variable ${1:variableName} ' + ${1:variableName});
-->

* __sds__ : system.debug for a selected variable
<!--
System.debug(' variable ${1:TM_SELECTED_TEXT} ' + ${1:TM_SELECTED_TEXT});
-->






### Visualforce Code Snippets


### Aura Components Code Snippets

##### Componnet tags


* __aattrib__ : Aura lighting attribute tag
<!--code snippet generator 
  <aura:attribute name="${1:sobject}" type="${2|String,Number,Date|}" default="${3:defaultvalue}"/>
-->

* __abutton__ : aura lightning button
<!--code snippet generator 
<lightning:button variant="${1|base,Neutral,brand,destructive,success|}" label="${2:label}" title="${3:title}" onclick="{!c.${4:sobject}}"/>",
  
-->
* __aNumber__ : aura lightnign number input
<!--code snippet generator 
  		  <lightning:input type="number" name="${1:name}" label="${2:label}" required=\${3|true,false|}" value="${3:value}" />"

-->



* __iter__ : aura iteration loop
<!--code snippet generator 
  <aura:iteration items="{!v.${1:listVariableName}}" var="${1:var}">
  $0
</aura:iteration>
-->


#### Controller, Helper and Design

* __call_apex__ : call apex class method from controller or helper
call apex class method from controller or helper
<!--code snippet generator 
         var ${1:actionName}= component.get("c.${2:apexMethodName}"");
        ${1:actionName}.setCallback(this, function(response) {
            var state = response.getState();
            if (state === "SUCCESS") {
                $0
            }            
        });
        $A.enqueueAction(${1:actionName});
-->

* __call_apex_full__ : call apex class method from controller or helper with the excpetion handling
call apex class method from controller or helper with the excpetion handling
<!--code snippet generator 
        var action = cmp.get("c.${1:apexMethodName}");
        action.setParams(
                    { ${2:apexParameterName}: cmp.get("v.${3:componentVarName}") }
                 );

        // set Callback
        action.setCallback(this, function(response) {
            var state = response.getState();
            if (state === "SUCCESS") {
                // TODO: Business Logic to be executed on Success
                 $0
            } else if (state === "ERROR") 
            {
               // TODO: Business Logic to be executed on Error
                var errors = response.getError();
                if (errors) 
                 {
                    if (errors[0] && errors[0].message) {
                       console.log("Error message: " + errors[0].message);
                    }
                } else {
                    console.log("Unknown error");
                }
            }
        });
        \$A.enqueueAction(action);
-->




