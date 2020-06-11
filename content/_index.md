+++
title = "Time-fluid Field-based Coordination by Danilo Pianini"
outputs = ["Reveal"]

[reveal_hugo]
width = '90%'
height = '100%'
theme = "black"

+++

{{< slide background-image="assets/flow.jpg" state="blur-animation"  transition="fade-in fade-out" >}}

<script src="prism.js"></script>
<script type="text/javascript"
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
<link rel="stylesheet" href="prism.css">
<link rel="stylesheet" href="blur.css">

<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  tex2jax: {
    inlineMath: [['$','$'], ['\\(','\\)']],
    displayMath: [['$$','$$'], ['\[','\]']],
    processEscapes: true,
    processEnvironments: true,
    skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
    TeX: { equationNumbers: { autoNumber: "AMS" },
         extensions: ["AMSmath.js", "AMSsymbols.js"] }
  }
});
</script>

<script type="text/x-mathjax-config">
  MathJax.Hub.Queue(function() {
    // Fix <code> tags after MathJax finishes running. This is a
    // hack to overcome a shortcoming of Markdown. Discussion at
    // https://github.com/mojombo/jekyll/issues/199
    var all = MathJax.Hub.getAllJax(), i;
    for(i = 0; i < all.length; i += 1) {
        all[i].SourceElement().parentNode.className += ' has-jax';
    }
});
</script>

# [Time-fluid field-based coordination](https://danysk.github.io/Slides-2020-Coordination-TimeFluid/)

__Danilo Pianini__, Stefano Mariani

Mirko Viroli, Franco Zambonelli

---

{{< slide background-image="assets/clocks.jpg" state="blur-animation"  transition="fade-in fade-out" >}}

# What is time?

---

{{< slide background-image="assets/clocks.jpg" state="blur-animation"  transition="fade-in fade-out" >}}

# Does time even exist?

---

{{< slide background-image="assets/clocks.jpg" state="blur-animation"  transition="fade-in fade-out" >}}

# Between physics and philosophy

## *Pre-relativity*

* Immutable
* Everywhere
* Fine for many practical applications, but does not match reality

---

{{< slide background-image="assets/relativity.jpg" state="blur-animation"  transition="fade-in fade-out" >}}

# Between physics and philosophy

## *Modern views*

* Very much related to the search for a unifying theory
* Several (conflicting) positions

**Suggested readings**

* Carroll's *From eternity to here*
* Rovelli's *The order of time*

---

{{< slide background-image="assets/relativity.jpg" state="blur-animation" transition="fade-in fade-out" >}}

# Relational interpretation
## Quantum systems are observer-dependent


> time might be meaningful only in presence of **_events_**

> time comes from **causality** and not vice versa

---

{{< slide background-image="assets/networking.jpg" state="blur-animation"  transition="fade-in fade-out">}}

# Field based coordination

### Computing by evolving distributed data structures:
### *computational fields*

#### Notable examples (not exhaustive):

* **TOTA** (Mamei/Zambonelli)
* **Fixpoint-based computational fields** (Lafuente/Loreti/Montanari)
* **Aggregate computing** (Beal/Pianini/Viroli)

---

{{< slide background-image="assets/networking.jpg" state="blur-animation"  transition="fade-in fade-out">}}

# Field based coordination

## *Dealing with time*

* The designer focuses on the **eventual behaviour**
* Computation happens in **atomic rounds**
* Round scheduling is controlled **externally**
* Scheduling may be:
  * **reactive** e.g., in *TOTA*
  * **proactive**/**timed** e.g., in *Aggregate computing*
  * **abstracted away** e.g., in *Fixpoint-based computational fields*

---

{{< slide background-image="assets/networking.jpg" state="blur-animation"  transition="fade-in fade-out">}}

# Field based coordination

## *Dealing with time*

* Historical focus on **space** rather than time
* Time is **abstracted away**  by design whenever possible

*...but in practice...*

* Space and time are **intertwined**
* **Propagation** speed influences the **evolution** of fields
* Dynamic systems are always in a **transient state**

---

{{< slide background-image="assets/waves.jpg"  state="blur-animation"  transition="fade-in fade-out">}}

# Challenge and desiderata

## *why bother?*

Fine grained control over **transient dynamics** \
enables improved **reactivity** to changes as well as **efficiency** \
both in *communication* and *energy consumption*

## *Requirement*

* **do not** force the designer to **lower** the **abstraction level**
* **do** support **all the existing** coordination mechanisms
* **do** allow for **proactive** and **reactive** policies 

---

{{< slide background-image="assets/waves.jpg"  state="blur-animation"  transition="fade-in fade-out">}}

# Time-Fluid Field Coordination

> leverage *field-based coordination itself* and maintain a\
**causality field** \
driving the dynamics of application-level fields

---

{{< slide background-image="assets/waves.jpg"  state="blur-animation"  transition="fade-in fade-out">}}

# Time-Fluid Field Coordination

* Define a set of **platform triggers `$ \mathcal{T} $`**
  * including *timers* and *results of field computations*
* Associate a **guard policy `$ \mathbf{G} $`** to every **field program `$ \mathbf{P} $`**
  * *inheriting the language* of the field program itself
  * **`$ \mathbf{G} $`**'s evaluation produces a *boolean* **`$b$`** and a *set* **`$T_c\subseteq\mathcal{T}$`** 
    * **`$b$`** determines whether **`$ \mathbf{P} $`** should *execute immediately*
    * **`$T_c$`** is the **causality field**
  * **`$ \mathbf{P} $`** will get *evaluated next* if an *event `$t\in$`* **`$T_c$`** happens
* At bootstrap, all policies are evaluated.

---

{{< slide background-image="assets/waves.jpg"  state="blur-animation"  transition="fade-in fade-out">}}

# Time-Fluid Field Coordination

**`$ \mathbf{P} $`** produces a local field value by consuming:
  * *messages* from neighbors *`$M\in\mathcal{M}$`*
  * *contextual information* (e.g., sensor readings) *`$S\in\mathcal{S}$`*

**`$ \mathbf{G} $`** is a field computation locally modeled as:
**`$$f_G\colon{}(\mathcal{S}, \mathcal{M})\to(\{0, 1\}, \mathcal{T}^{2})$$`**
* Access to *`$M$`* and *`$S$`* and the ability to produce  **`$T_c\in\mathcal{T}^{2}$`**\
  have crucial impact on the expressivity of **`$ \mathbf{G} $`**

---

{{< slide background-image="assets/waves.jpg"  state="blur-animation"  transition="fade-in fade-out">}}

# Time-Fluid Field Coordination

## Consequences

* From programming *space **in** time* to programming _**the** space-time_
  * Adaptation *controls* time rather than *experience* it
* **Adaptatation to causality** by reacting to perceived events
  * e.g., by *accelerating* or *slowing down* the field computation
* **Co-causality** as field computations can depend on each other
  * Of course, with great *expressiveness* comes great responsibility

---

{{< slide background-image="assets/dark.jpg"  state="blur-animation"  transition="fade-in fade-out">}}

# Time-Fluid Aggregate Computing

Prototype implementation [available](https://github.com/DanySK/Experiment-2020-Coordination-Time-Fluid-AC) using the [Protelis](http://www.protelis.org) programming language

* *No change* to the syntax of Protelis
* Aggregate computations have an associated *guard policy*
* Guard policies are written in *plain Protelis*

---

{{< slide background-image="assets/dark.jpg"  state="blur-animation"  transition="fade-in fade-out">}}

## Time-Fluid Aggregate Computing

*guard policy* code sample (more in the paper...)

```groovy
import platform.EventType.* // Event types are provided by the hosting platform
let reason = env.get("platform.event") // Sensor-like access to the triggering event
// Policy guards are full fledged aggregate programs
let peopleCount = foldSum(nbr(env.get("people_count")))
let lastCount = rep(s <- [0, 0]) { [s.get(1), peopleCount] }.get(0)
let attendantsChanged = lastCount != peopleCount
[ // A policy returns a pair of:
  // A boolean, deciding whether the guarded program should run
  reason == MESSAGE_TIMEOUT || reason == MESSAGE_RECEIVED || attendantsChanged,
  [MESSAGE_RECEIVED, SENSOR("people_count")] // A list of accepted future triggering events
]
```

---

{{< slide background-image="assets/dark.jpg"  state="blur-animation"  transition="fade-in fade-out">}}

### Evaluation

<img src="assets/network-2.svg" width="50%" height="50%" />

---

{{< slide background-image="assets/dark.jpg"  state="blur-animation"  transition="fade-in fade-out">}}

### Scenario

* 40x40 irregular grid of devices with the goal of computing *distance from* the closest *source*
* Sources are *mobile devices* and *one static* device located on South-West of the scenario
* Mobile devices enter one at a time from North-West and exit from North-East
* Devices *round frequency* is *dynamically* regulated via a *guard policy*

### Variables
* **f** --- maximum allowed frequency
* **v** --- speed of the mobile nodes

### Metrics
* **Error** --- Measured with respect to an oracle
* **Mean round count** --- Proxy metric for energy consumption


---

{{< slide background-image="assets/dark.jpg"  state="blur-animation"  transition="fade-in">}}

#### <span style="color:yellow">Yellow: less rounds</span> --- <span style="color:red">red: more rounds</span>

<img src="assets/freq01.png" width="50%" height="50%" />

---

{{< slide background-image="assets/dark.jpg"  state="blur-animation"  transition="fade-out">}}

#### <span style="color:yellow">Yellow: less rounds</span> --- <span style="color:red">red: more rounds</span>

<img src="assets/animation.gif" width="50%" height="50%" />

---

{{< slide background-image="assets/dark.jpg"  state="blur-animation"  transition="fade-in fade-out">}}

### Speed = 0

<img src="assets/rounds_speed0.pdf.svg" width="40%"/>
<img src="assets/error_speed0.pdf.svg" width="40%"/>

similar error, much lower energy cost

---

{{< slide background-image="assets/dark.jpg"  state="blur-animation"  transition="fade-in fade-out">}}

### Speed = 2

<img src="assets/rounds_speed2.pdf.svg" width="40%"/>
<img src="assets/error_speed2.pdf.svg" width="40%"/>

lower error *and* energy cost

---

{{< slide background-image="assets/dark.jpg"  state="blur-animation"  transition="fade-in fade-out">}}

### Speed = 5

<img src="assets/rounds_speed5.pdf.svg" width="40%"/>
<img src="assets/error_speed5.pdf.svg" width="40%"/>

lower error *and* energy cost

---

{{< slide background-image="assets/dark.jpg"  state="blur-animation"  transition="fade-in fade-out">}}

### Speed = 10

<img src="assets/rounds_speed10.pdf.svg" width="40%"/>
<img src="assets/error_speed10.pdf.svg" width="40%"/>

lower error *and* energy cost

---

{{< slide background-image="assets/flow.jpg" state="blur-animation"  transition="fade-in fade-out" >}}

# Time-Fluid Field Coordination

## Conclusion

* A **causality field** approach for programming **the** space-time
* Inherits the *host language*
* Applicable to *field-based coordination* approaches
* *Prototype available* for Aggregate Computing / Protelis

## Future work

* *Develop* the prototype to general availability 
* *Test* impact on real network