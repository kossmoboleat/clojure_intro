class: center, middle

# Clojure - The Average Joe's Lisp

![alt text](https://imgs.xkcd.com/comics/lisp.jpg "XKCD Lisp")

from [xkcd](https://xkcd.com/224/)

---
.left-column[
## Agenda
]
.right-column[
1. Syntax 101

2. Short Demo

3. Teaser of language features

4. Clojure for the Web

5. Workflow Demo
]
---

.left-column[
## Syntax 101
### *-example*
]
.right-column[
```clojure
(ns clojureintro)

(+ 1 1)
=> 2

(defn hello [name]
  (str "Hello " name))
=> #'user/hello

(hello "Tim")
=> "Hello Tim"

(defn odd-numbers [max]
  (filter odd? (range max)))
=> #'user/odd-numbers

(odd-numbers 10)
=> (1 3 5 7 9)

(def keymap {:a 1, :b 2, :c 3})
=> #'user/keymap

(keymap :a)
=> 1
```
]

---

class: center, middle

![all the syntax](https://i.imgflip.com/1buw2j.jpg)

---

.left-column[
## Syntax 101
### *-example*
### *-primitives*
]
.right-column[

- Integers `12345678`

- Doubles `1.234`, BigDecimals `1.2345M`

- .red.bold[Ratios `17/4`]

- Strings `"fred"`

- .red.bold[Symbols `fibonacci`], Keywords `:fred`

- Boolean `true` `false`, .red.bold[null `nil`]

- Regex Patterns `#"a*b"`
]
---

.left-column[
## Syntax 101
### *-example*
### *-data types*
### *-data structures*
]
.right-column[
 - Lists - singly linked, grow at front

`(1 2 3 4 5), (fred ethel lucy), (list 1 2 3)`

 - Vectors - indexed access, grow at end

`[1 2 3 4 5], ["fred" "ethel" "lucy"]`

 - Maps - key-value associations

`{:a 1, :b 2, :c 3}, {1 "ethel" 2 "fred"}`

- Sets

`#{fred ethel lucy}`
]

???
Everything Nests

All types support mixed key and value types

---

.left-column[
## Syntax 101
### *-example*
### *-primitives*
### *-data structures*
### *-persistent & immutable*
]
.right-column[
- Persistent and immutable

- Same amortized complexity

- Plethora of collection functions
]
---

class: center, middle

# Demo

???
# REPL

- run code from file

# data structures

- Representation = Initialization syntax
- Serialization to EDN

# key shortcuts

Toggle Presentation Mode - hyper+p  
Go to REPL - hyper+r  
Maximize/Restore Tool Window - hyper+m  
Reload file in REPL - hyper+k  

---

.left-column[
## Language
### *-a LISP?*
]
.right-column[
- LISP specified in 1958

- first stable release of Clojure in 2009

- runs on the JVM (and .NET VM CLR)

- sister language Clojurescript that transpiles to Javascript
]

???
- designed by Rich Hickey

---

.left-column[
## Language
### *-a LISP?*
]
.right-column[
# Same

- Syntax and Code-as-data (Homoiconic)

- Dynamic & Functional

# Different

- no user defined reader macros

- not compatible with Common Lisp

- literals for lists () plus maps {} and vectors []
]

???

- Homoiconic = good for macros

---

.left-column[
## Language
### *-a LISP?*
### *-performance*
]
.right-column[
- about as fast as Java

- faster than Python, Javascript, Ruby, Common Lisp

- same slow startup as everything on the JVM
]

---

.left-column[
## Language
### *-a LISP?*
### *-performance*
### *-OO*
]
.right-column[
- protocols (similar to interfaces) for existing classes, even final like String

- records for data - compatible to maps

- multimethods for polymorphism++
]

???

- multimethods = "multiple dispatch"

---

.left-column[
## Language
### *-a LISP?*
### *-performance*
### *-OO*
### *-dynamic*
]
.right-column[
- dynamic strong typed language

- type errors vs. quality; static typing + tests

- optional/gradual typing available: [core.typed](https://github.com/clojure/core.typed)

- types + validator with [clojure spec](http://clojure.org/guides/spec)


```clojure
(def email-regex #"^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,63}$")
(s/def ::email-type (s/and string? #(re-matches email-regex %)))

(s/def ::acctid int?)
(s/def ::first-name string?)
(s/def ::last-name string?)
(s/def ::email ::email-type)

(s/def ::person (s/keys :req [::first-name ::last-name ::email]
                        :opt [::phone]))
```
]

???
- Predecessor: prismatic/plumatic schema

---

.left-column[
## Language
### *-a LISP?*
### *-performance*
### *-OO*
### *-dynamic*
### *-functional*
]
.right-column[
- "Automatic tail call optimization is not supported as the JVM", possible with `recur` [1](https://www.youtube.com/watch?v=2y5Pv4yN0b0&t=1h02m18s) [2](https://en.wikipedia.org/wiki/Clojure)
  
  - Brian Goetz: "It's not the highest priority [..] but we will eventually get there."

- lazy infinite sequences > Java streams

- macros

```clojure
(when true "Hello")
=> "Hello"
(when false "Hello")
=> nil

(defmacro unless [arg & body]
  `(if (not ~arg)
     (do ~@body)))

(unless false "Hello")
=> "Hello"
(unless true "Hello")
=> nil
```
]
---

.left-column[
## Language
### *-a LISP?*
### *-performance*
### *-OO*
### *-dynamic*
### *-functional*
### *-concise*
]
.right-column[
- very concise syntax, e.g. anonymous fn's: `#(= "TUI")`

- value objects are just data

- Java `javax.servlet.http.HttpServletRequest`

```java
getAsyncContext, getAttribute, getAttributeNames, 
getCharacterEncoding, getContentLength, 
getContentLengthLong, getContentType, getDispatcherType, 
getInputStream, getLocalAddr, getLocale, 
getLocales, getLocalName, getLocalPort, getParameter, 
getParameterMap, getParameterNames, 
getParameterValues, getProtocol ... 
```

[//]: # (getAsyncContext, getAttribute, getAttributeNames, getCharacterEncoding, getContentLength, getContentLengthLong, getContentType, getDispatcherType, getInputStream, getLocalAddr, getLocale, getLocales, getLocalName, getLocalPort, getParameter, getParameterMap, getParameterNames, getParameterValues, getProtocol, getReader, getRealPath, getRemoteAddr, getRemoteHost, getRemotePort, getRequestDispatcher, getScheme, getServerName, getServerPort, getServletContext, isAsyncStarted, isAsyncSupported, isSecure, removeAttribute, setAttribute, setCharacterEncoding, getAuthType, getContextPath, getCookies, getDateHeader, getHeader, getHeaderNames, getHeaders, getIntHeader, getMethod, getPart, getParts, getPathTranslated, getQueryString, getRemoteUser, getRequestedSessionId, getRequestURI, getRequestURL, getServletPath, getSession, getUserPrincipal, isRequestedSessionIdFromCookie, isRequestedSessionIdFromUrl, isRequestedSessionIdFromURL, isRequestedSessionIdValid(), isUserInRole)

- Clojure ring libray http `request`

```clojure
{
:content-length 100
:parameters {"user" "tim" "pass" "secret"}
:uri "http://www.meetup.com/Hannover-FP/"
...
}
```
]

???
- smaller size -> less bugs

---

.left-column[
## Language
### *-a LISP?*
### *-performance*
### *-OO*
### *-dynamic*
### *-functional*
### *-concise*
### *-Java interop*
]
.right-column[
- mostly the same primitives (numbers, chars, strings)

- data structures implement Java Collection interfaces

- easy to access Java libraries

- inherits "write once, run anywhere"
]

???
- many popular libraries wrap existing battle-tested code, e.g for security
- similar deployment as war or jar with embedded web server
---

class: center, middle

![web of parentheses](https://i.imgflip.com/1buwin.jpg)

---

.left-column[
## Web-Dev
### *-HTML DSL*
]
.right-column[

- easy to create DSLs like hiccup

```clojure
[:div {:class "well"}
   [:h1 {:class "text-info"} "Hello Hiccup and"]
   [:div {:class "row"}
    [:div {:class "col-lg-2"}
     (label "name" "Name:")]
    [:div {:class "col-lg-4"}
     [:input {:placeholder "Enter name here"} ]]
   [:hr]]]
```
]

---

.left-column[
## Web-Dev
### *-HTML DSL*
### *-Tooling*
]
.right-column[

## Build Tools

- [Leinigen](http://leiningen.org/)=Maven and [Boot](http://boot-clj.com/)=Gradle
  - both tap into the maven repository

## Editors and IDEs 

- [cursive](https://cursive-ide.com/) plugin for intellij, 
- [emacs](https://github.com/clojure-emacs/cider), [vim](https://github.com/guns/vim
-clojure-static) [2](https://github.com/tpope/vim-fireplace)
- [counterclockwise](http://doc.ccw-ide.org/) -plugin for eclipse, 
- [lighttable](http://lighttable.com/)

## Interactive Programming

- [figwheel](https://www.youtube.com/watch?v=KZjFVdU8VLI)
]

---

.left-column[

## Web-Dev
### *-HTML DSL*
### *-Tooling*
### *-Libraries*
]
.right-column[

- Libraries instead of frameworks

## Backend

- compojure for the backend which builds on ring

- thin SQL wrappers instead of ORM

  - korma, yesql or Clojure's JDBC


## Frontend

- reagent (and om) are clojure wrappers for react

- Google closure optimizes code 

- "isomorphic" code (used in frontend and backend)

- Javascript interop from Clojurescript

]

???
- reagent (and om) are clojure wrappers for react

  - many concepts overlap with functional programming

  - immutable

  - redux vs central state atom

- name pearls
  - security libs friend & buddy

  - XML-RPC lib [necessary evil](https://github.com/brehaut/necessary-evil)

- arachne web framework [discussion](http://arachne-framework.org/posts/2016/frameworks-libraries-and-templates/) 

---

class: center, middle

# Demo

---

#Prominent Supportes

- Uncle Bob / Robert C. Martin: [Clojure Is the New C](https://www.infoq.com/presentations/clojure-c), [Why Clojure?](http://thecleancoder.blogspot.de/2010/08/why-clojure.html)

- Roomkey

- Netflix

- Walmart

- verizon

- IBM

- BBC

---

#Stewardship

- first version developed by Rich Hickey

- language is open source

- community driven development process

- Cognitect was founded by Hickey and Stu Halloway

- Cognitect consults and build Clojure applications

- they also produce a database called datomic

---


#References

- [Programming Clojure by Stuart Halloway](https://pragprog.com/book/shcloj/programming-clojure)
- [Web Development with Clojure](https://pragprog.com/book/dswdcloj2/web-development-with-clojure-second-edition)
- [Cognicast Podcast](http://blog.cognitect.com/cognicast/)
- Video ["Expert to Expert: Erik Meijer and Rich Hickey - Clojure and Datomic"](https://www.youtube.com/watch?v=8uHfMltTbqs)
- Rick Hickey talks:
  - [Clojure, made simple](https://www.youtube.com/watch?v=VSdnJDO-xdg)
  - [Hammock driven development](https://www.youtube.com/watch?v=f84n5oFoZBc)
- talk ["Why Clojure?"](https://www.youtube.com/watch?v=SLRSOyR47Ro) by Vijay Kiran
- [ClojureDocs](http://clojuredocs.org/)
- [Online-REPL](http://www.tryclj.com/)
- [Interactive Clojure problems](http://www.4clojure.com/)
- State of Clojure Survey 2015 [results](http://blog.cognitect.com/blog/2016/1/28/state-of-clojure-2015-survey-results)
- Uncle Bob / Robert C. Martin: [Clojure Is the New C](https://www.infoq.com/presentations/clojure-c), [Why Clojure?](http://thecleancoder.blogspot.de/2010/08/why-clojure.html)