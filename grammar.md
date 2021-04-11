# Grammar

### Grammar Notation

```text
Result  ::= component1 ( component2 | component3 ) | 
            component4 | [component5] component6
- /* comments */
- 'literal'
- (A|B): either of A or B
- A B: A then B
- [A]: Optional A
- (A)* : Repeating A zero or more times
- (A)+ : Repeating A one or more times
- {A}*  : Repeating A zero or more times, separated with comma
- {A}+  : Repeating A one or more times, separated with comma
```

### Top-level

A module is a series of types \(named or alias\) or bindings \(value or function\).

```text
Module                   ::= ( TypeDecl | BindingDecl )*
```

### Naming basics

```text
TypeName                ::= CAPITAL_LETTER (ALPHABET)*
BindingName             ::= ValueBindingName | TypeName | FunctionName
ValueBidningName        ::= (LOWERCASE) (LOWECASE | '_')*
FunctionName            ::= LOWERCASE (LOWERCASE | CAPITAL_LETTER)*
ModuleAlias             ::= ValueBidningName
```

### Type Declaration

Declaration of a named type or type alias

```text
TypeDecl                ::= TypeName (':'|'=') TypeLiteral
TypeLiteral             ::= PrimitiveType | StructType | UnionType | 
                            FnType | SeqType | MapType | EnumType | 
                            TypeName
PrimitiveType           ::= 'int' | 'float' | 'string' | 'char' | 
                            'byte' | 'bool' | 'nothing'
StructType              ::= 'struct' '{' {StructField}* '}'
StructField             ::= { Identifier ':' TypeLiteral }
UnionType               ::= (TypeLiteral '|' TypeLiteral) | (TypeLiteral '|' UnionType)
FnType                  ::= 'fn' '(' { TypeLiteral }* '->' { TypeLiteral }* ')'
SeqType                 ::= '[' TypeLiteral ']'
MapType                 ::= '[' TypeLiteral ':' TypeLiteral ']'
EnumType                ::= 'enum' SeqLiteral
```

### Binding Declaration

Types of expressions you can define by combining other expressions \(mathematical, struct access, boolean, a function call, ...\).

```text
BindingDecl             ::= { BindingNameItem }* '=' Expression
BindingNameItem         ::= BindingName [ ':' Type ] | '_'
Expression              ::= EqExpression     { ('and'|'or') EqExpression }*
EqExpression            ::= CmpExpression    { ('=='|'!=') CmpExpression }*
CmpExpression           ::= ShiftExpression  { ('>'|'<'|'>='|'<=') 
                                ShiftExpression }*
ShiftExpression         ::= AddExpression    { ('>>'|'<<'|'^') 
                                AddExpression }*
AddExpression           ::= MulExpression    { ('+'|'-') 
                                MulExpression }*
MulExpression           ::= UnaryExpression  { ('*'|'/'|'%'|'%%') 
                                UnaryExpression }*
UnaryExpression         ::= ['not'|'-']      BasicExpression
BasicExpression         ::= ['('] PrimaryExpression [')']
PrimaryExpression       ::= Literal | 
                                Identifier | 
                                StructAccessExpression | 
                                MapSeqAccessExpression | 
                                FnCallExpression | 
                                StructExpression | 
                                LambdaCreatorExpression | 
                                FnDeclaration |
                                IfExpression | 
                                ElseExpression | 
                                ErrorCheckExpression
StructAccessExpression  ::= Expression '.' Identifier
MapSeqAccessExpression  ::= Expression '[' Expression ']'
FnCallExpression        ::= Expression '(' { Expression }* ')'
StructExpression        ::= ( TypeName | StructType | '&' ) 
                                '{' {FieldValueList}* '}'
FieldValueList          ::= { [ Identifier ':' ] Expression }
LambdaCreatorExpression ::= Expression '(' { Expression | '_' }* ')'
FnDeclaration           ::= 'fn' ['(' { Identifier ':' Type } 
                                '->' {Type}+ ')'] '{' Expression+ '}'
IfExpression            ::= Expression '?' Expression
ElseExpression          ::= Expression '//' Expression
ErrorCheckExpression    ::= Expression '@' [ '{' Expression '}' ]
Literal                 ::= IntLiteral | 
                                FloatLiteral | 
                                CharLiterl | 
                                StringLiteral | 
                                NothingLiteral | 
                                BoolLiteral | 
                                SeqLiteral | 
                                MapLiteral | 
                                StructLiteral | 
                                TypeLiteral
```

## To Be Added Later

* Generics
* Concurrency and channels 
* Modules and import

