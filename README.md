<img src="https://mobx.js.org/assets/mobx.png" alt="logo" height="120" align="right" />

# MobX

_Simple, scalable state management._

[![npm version](https://badge.fury.io/js/mobx.svg)](https://badge.fury.io/js/mobx)
[![OpenCollective](https://opencollective.com/mobx/backers/badge.svg)](docs/backers-sponsors.md#backers)
[![OpenCollective](https://opencollective.com/mobx/sponsors/badge.svg)](docs/backers-sponsors.md#sponsors)
[![Discuss on Github](https://img.shields.io/badge/discuss%20on-GitHub-orange)](https://github.com/Unity-Billal-mesloub/mobx/discussions)
[![Coverage Status](https://coveralls.io/repos/github/mobxjs/mobx/badge.svg?branch=main)](https://coveralls.io/github/mobxjs/mobx?branch=main)
[![View changelog](https://img.shields.io/badge/changelogs.xyz-Explore%20Changelog-brightgreen)](https://changelogs.xyz/mobx)

---

## Documentation

Documentation can be found at **[mobx.js.org](https://mobx.js.org/)**.

---

## Introduction

_Anything that can be derived from the application state, should be. Automatically._

MobX is a signal based, battle-tested library that makes state management simple and scalable by transparently applying functional reactive programming.
The philosophy behind MobX is simple:

<div class="benefits">
    <div>
        <div class="pic">😙</div>
        <div>
            <h4>Straightforward</h4>
            <p>Write minimalistic, boilerplate-free code that captures your intent.
            Trying to update a record field? Simply use a normal JavaScript assignment —
            the reactivity system will detect all your changes and propagate them out to where they are being used.
            No special tools are required when updating data in an asynchronous process.
            </p>
        </div>
    </div>
    <div>
        <div class="pic">🚅</div>
        <div>
            <h4>Effortless optimal rendering</h4>
            <p>
                All changes to and uses of your data are tracked at runtime, building a dependency tree that captures all relations between state and output.
                This guarantees that computations that depend on your state, like React components, run only when strictly needed.
                There is no need to manually optimize components with error-prone and sub-optimal techniques like memoization and selectors.
            </p>
        </div>
    </div>
    <div>
        <div class="pic">🤹🏻‍♂️</div>
        <div>
            <h4>Architectural freedom</h4>
            <p>
                MobX is unopinionated and allows you to manage your application state outside of any UI framework.
                This makes your code decoupled, portable, and above all, easily testable.
            </p>
        </div>
    </div>
</div>

---

## A quick example

So what does code that uses MobX look like?

```javascript
import React from "react"
import ReactDOM from "react-dom"
import { makeAutoObservable } from "mobx"
import { observer } from "mobx-react-lite"

// Model the application state.
const myTimer = makeAutoObservable({
    secondsPassed: 0,
    increase() {
        this.secondsPassed += 1
    },
    reset() {
        this.secondsPassed = 0
    }
})

// Build a "user interface" that uses the observable state.
const TimerView = observer(({ timer }) => (
    <button onClick={() => timer.reset()}>Seconds passed: {timer.secondsPassed}</button>
))

ReactDOM.render(<TimerView timer={myTimer} />, document.body)

// Update the 'Seconds passed: X' text every second.
setInterval(() => {
    myTimer.increase()
}, 1000)
```

The `observer` wrapper around the `TimerView` React component will automatically detect that rendering
depends on the `timer.secondsPassed` observable, even though this relationship is not explicitly defined. The reactivity system will take care of re-rendering the component when _precisely that_ field is updated in the future.

Every event (`onClick` / `setInterval`) invokes an _action_ (`myTimer.increase` / `myTimer.reset`) that updates _observable state_ (`myTimer.secondsPassed`).
Changes in the observable state are propagated precisely to all _computations_ and _side effects_ (`TimerView`) that depend on the changes being made.

<img alt="MobX unidirectional flow" src="https://mobx.js.org/assets/flow2.png" align="center" />

This conceptual picture can be applied to the above example, or any other application using MobX.

## Getting started

To learn about the core concepts of MobX using a larger example, check out **[The gist of MobX](https://mobx.js.org/the-gist-of-mobx.html)** page, or take the **[10 minute interactive introduction to MobX and React](https://mobx.js.org/getting-started)**.
The philosophy and benefits of the mental model provided by MobX are also described in great detail in the blog posts [UI as an afterthought](https://michel.codes/blogs/ui-as-an-afterthought) and [How to decouple state and UI (a.k.a. you don’t need componentWillMount)](https://hackernoon.com/how-to-decouple-state-and-ui-a-k-a-you-dont-need-componentwillmount-cc90b787aa37).

## Further resources

-   The [MobX cheat sheet](https://gum.co/fSocU) (£5) is both useful and sponsors the project
-   [10 minute interactive introduction to MobX and React](https://mobx.js.org/getting-started)
-   [Egghead.io course, based on MobX 3](https://egghead.io/courses/manage-complex-state-in-react-apps-with-mobx)

### The MobX book

<a href="https://www.packtpub.com/product/mobx-quick-start-guide/9781789344837"><img src="https://mobx.js.org/assets/book.jpg" height="120px" /></a>

The **[MobX Quick Start Guide](https://www.packtpub.com/product/mobx-quick-start-guide/9781789344837)** ($24.99) by [Pavan Podila](https://www.packtpub.com/product/mobx-quick-start-guide/9781789344837), [paperback](https://www.amazon.com/MobX-Quick-Start-Guide-Supercharge/dp/1789344832), and on the [O'Reilly platform](https://www.oreilly.com/library/view/mobx-quick-start/9781789344837/) (see [preview](https://books.google.com/books?id=ALFmDwAAQBAJ&printsec=frontcover#v=onepage&q&f=false)).

### Videos

-   [Introduction to MobX & React in 2020](https://www.youtube.com/watch?v=pnhIJA64ByY) by Leigh Halliday, _17 min_.
-   [ReactNext 2016: Real World MobX](https://www.youtube.com/watch?v=Aws40KOx90U) by Michel Weststrate, _40 min_, [slides](https://docs.google.com/presentation/d/1DrI6Hc2xIPTLBkfNH8YczOcPXQTOaCIcDESdyVfG_bE/edit?usp=sharing).
-   [CityJS 2020: MobX, from mutable to immutable, to observable data](https://youtu.be/sP7dtZm_Wx0?t=27050) by Michel Weststrate, _30 min_.
-   [OpenSourceNorth: Practical React with MobX (ES5)](https://www.youtube.com/watch?v=XGwuM_u7UeQ) by Matt Ruby, _42 min_.
-   [HolyJS 2019: MobX and the unique symbiosis of predictability and speed](https://www.youtube.com/watch?v=NBYbBbjZeX4&list=PL8sJahqnzh8JJD7xahG5zXkjfM5GOgcPA&index=21&t=0s) by Michel Weststrate, _59 min_.
-   [React Amsterdam 2016: State Management Is Easy](https://www.youtube.com/watch?v=ApmSsu3qnf0&feature=youtu.be) by Michel Weststrate, _20 min_, [slides](https://speakerdeck.com/mweststrate/state-management-is-easy-introduction-to-mobx).
-   {🚀} [React Live 2019: Reinventing MobX](https://www.youtube.com/watch?v=P_WqKZxpX8g) by Max Gallo, _27 min_.

## Credits

MobX is inspired by reactive programming principles, which are for example used in spreadsheets. It is inspired by model–view–viewmodel frameworks like [MeteorJS's Tracker](https://docs.meteor.com/api/tracker.html), [Knockout](https://knockoutjs.com/) and [Vue.js](https://vuejs.org/), but MobX brings _transparent functional reactive programming_ (TFRP, a concept which is further explained in the [MobX book](https://www.packtpub.com/product/mobx-quick-start-guide/9781789344837)) to the next level and provides a standalone implementation. It implements TFRP in a glitch-free, synchronous, predictable and efficient manner.

A ton of credit goes to [Mendix](https://github.com/Unity-Billal-mesloub), for providing the flexibility and support to maintain MobX and the chance to prove the philosophy of MobX in a real, complex, performance critical applications.
