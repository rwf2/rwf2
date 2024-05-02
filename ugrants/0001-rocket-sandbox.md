---
title: Rocket Sandbox
date: 2024-06-21
issue: rwf2/rwf2#10
---

# Summary
[summary]: #summary

This grant sponsors the development of a web application that receives untrusted
Rocket application source code and executes it in a sandboxed environment,
returning the compilation and execution results. The goal is to enable
functionality similar to the [Rust playground] but for Rocket applications. The
application will power executable code in Rocket's documentation and enable new
learning tools including interactive tutorials and playgrounds.

The award is $1,000 USD distributed on milestones that progressively build
toward the desired application.

[Rust playground]: https://play.rust-lang.org/

# Motivation
[motivation]: #motivation

Rocket's documentation is the library's entry point for most developers and a
cornerstone of knowledge for existing developers. In order to help attract the
former and communicate more effectively with the latter, we seek to extend
Rocket's documentation with executable code.

Specifically, we want to enable:

  1. Making code examples in [Rocket's guide] executable directly from the
     documentation, similar to how the [`std` docs] allows users to run code
     snippets. The aim is to enable users to quickly test and understand
     Rocket's concepts.
  2. Interactive tutorials where the user can work through guided code examples
     on Rocket's website with the ability to run, debug, fix, and rerun their
     code. [Svelte's examples] exemplify the experience we're aiming for.
  3. Playgrounds where users can experiment by sending "requests" to Rocket
     applications written in-browser, allowing them to explore and learn about
     Rocket's capabilities in a hands-on manner.

[Rocket's guide]: https://rocket.rs/guide
[`std` docs]: https://doc.rust-lang.org/stable/std/macro.print.html#examples
[Svelte's examples]: https://svelte.dev/examples/hello-world

# Candidate Requirements
[requirements]: #requirements

The minimum requirements for a candidate are:

  * Ability to write idiomatic Rust.
  * Demonstrated understanding of sandboxing techniques and interfaces.
  * Knowledge of how Rust APIs interface with the OS (filesystem, networking,
    processes, etc.).
  * Ability and willingness to document how an implementation faithfully
    restricts untrusted code execution.

# Description
[description]: #description

The sandboxing web application provides a means to compile and run Rocket
applications in a securely isolated context. It exposes a minimal REST API that
allows myriad use cases including:

  - Receiving documentation code examples to run.
  - Executing prescriptive "tutorial" code.
  - Powering interactive "Rocket playgrounds".

In theory, the exposed REST API can be simplified to a single endpoint that
accepts three parameters:

  1. Stub source code to sandbox.
  2. An identifier for the [harness] to use when sandboxing.
  3. Arguments to the [harness], if any.

Upon receiving such a request, the application creates a restrictive sandbox
where it:

  1. Safely injects the stub into a harness.
  2. Compiles the resulting source code.
  3. Executes the resulting program, capturing and returning output.

## Harnesses
[harness]: #harnesses
[harnesses]: #harnesses

The submitted source code may be a _stub_ which cannot be executed directly and
instead expects to be injected into and executed as part of a harness. The
harness provides the necessary set-up and tear-down for the stub's execution and
allows the sandbox to be agnostic about the code it ultimately executes.

As an example, one harness may expect a stub that contains an `async` function
named `rocket` that returns a type of `Rocket<Build>`. Such a harness may
leverage the stub as follows:

```rust
fn main() {
    let rocket: Rocket<Build> = rocket().await;
    sandbox_execute(rocket);
}
```

A second harness may require three inputs: 1) the stub for a `Rocket<build>`, as
above, 2) an HTTP method as a string, and 3) a URI as a string. Such a harness
may leverage these inputs to execute a local HTTP request as follows:

```rust
fn main() -> Result<()> {
    use rocket::local::blocking::Client;

    let rocket: Rocket<Build> = rocket().await;
    let client = Client::tracked(rocket)?;
    let response = client.req(method, uri).dispatch()?;
    Ok(())
}
```

The sandboxing web application must be flexible enough to allow implementing
these types of harnesses and more.

## Security
[security]: #security

It is imperative that the web application properly sandbox the compilation and
execution of any untrusted source code to prevent a takeover of the sandboxing
machine. Concretely, it must restrict and limit access to all logical and
physical resources. This includes limiting or completely restricting access to
the OS, network, disk, CPU, memory, and all such derivatives such as randomness,
file descriptors, inodes, processes, and threads whenever it is operating on or
executing untrusted code or derivatives of untrusted code.

**Untrusted code** refers to any submitted source code as well as artifacts
derived from the source code including compilation and execution output. This
also includes the Rust compiler executed on any portion of submitted source code
or any derived intermediate output.

The **trusted code base** includes the Linux kernel, the web application itself,
and untainted harnesses, prior to stub injection.

## Performance
[performance]: #performance

To provide a good user experience, minimizing the time the user waits for output
is essential. To this end, the web application should implement the following
performance enhancements:

  * **Memoization**: The complete pipeline should be memoized based on a
    normalized triple of (source code, harness, input). This prevents performing
    any unnecessary work when the result is known. Note that this enhancement
    relies on deterministic execution, which the sandbox should enforce as much
    as realistically possible.
  * **Dependency caching**: Dependencies required to compile the injected
    harness should never be recompiled unnecessarily.
  * **Optimized compiler flags**: Compiler flags should be optimized for quick
    compilation to reduce end-to-end latency.

## Challenges

Implementing this proposal poses two primary challenges:

  1. **Selecting and vetting a suitable sandboxing technology.** This grant does
     not prescribe any particular technology, but it must meet certain criteria:
     it cannot require running services or daemons to function, and it should
     not incur a large performance penalty. We prefer technologies written in
     Rust that leverage Linux kernel facilities.

  2. **Identifying and resolving assumed access to resources.** The Rust
     compiler or Rocket or its dependencies may assume access to resources which
     may not be available in the sandboxed environment. This may inhibit
     sandboxed compilation or execution of Rocket applications. The assumptions
     and ensuing restrictions must be identified and resolved. A portion of this
     grant is dedicated to doing so in a general, reusable, and upstreamable
     manner.

# Goals & Non-Goals
[goals]: #goals

The application must:

  * Receive, compile, and safely/reliably execute untrusted Rocket applications
    inside trusted harnesses.
  * Be written in Rocket with Rust with minimal or no `unsafe` code.
  * Impose configurable, indelible limits on all resources during code execution
    (CPU, memory, PIDs, execution time, etc.).
  * Prohibit any/all external or persistent communication (network, disk, etc.).
  * Remove or deterministically virtualize all sources of non-determinism as
    much as possible.
  * Execute code in a stateless fashion: no unwanted execution state should
    remain after execution.
  * Be able to execute inside of a virtual machine.
  * Use minimal resources to allow running many untrusted programs in parallel
    on a lightweight machine.
  * Memoize and maintain a cache of past executions.

The application must not:

  * Incur extensive overhead to create sandboxed environments.
  * Allow escaping the sandbox in any way, ensuring complete isolation.
  * Rely on Docker or other container runtimes.
  * Require running services or daemons to function.
  * Recompile dependencies unnecessarily.

# Milestones & Deliverables
[milestones]: #milestones

  1. **Design and Implementation Plan**

     Present a concrete design and implementation plan that describes how and
     why executing the plan would meet the required goals and non-goals. The
     plan should also address the [security] and [performance] sections.

     **Deliverable:** A short document that 1) concretely selects sandboxing
     technology and describes how it meets the described goals and non-goals, 2)
     describes a concrete plan to implement harnessing support, and 3)
     identifies what changes, if any, need to be made to existing libraries like
     Rocket and `tokio`.

  2. **Sandboxed Compilation and Execution**

     Implement a simple Rocket application that receives fully harnessed source
     code, compiles, and executes it in a fully sandboxed environment and
     returns the result. The candidate can arbitrarily choose what "fully
     harnessed" means _as long as_ the fully harnessed source can be composed
     from a harness and an untrusted stub. An example of what "fully harnessed"
     source code might look like follows:

     ```rust
     #[macro_use] extern crate rocket;

     #[get("/")]
     fn hello() -> &'static str {
         "Hello, world!"
     }

     #[launch]
     fn rocket() -> _ {
         rocket::build().mount("/", routes![hello])
     }

     fn main() {
         use rocket::local::blocking::Client;

         let client = Client::tracked(rocket()).unwrap();
         let response = client.get("/").dispatch();
         println!("{:?}", response.into_string());
     }
     ```

     **Deliverables:**
       1. Pull requests with the necessary changes to existing libraries from
          milestone 1, if any.
       2. A pull request which contains fully documented source code for a
          Rocket application that performs the above.

  3. **Harness Support**

     Add support for harnesses with arguments. Modify the application such that
     it receives a (stub, harness id, inputs..) triple. The candidate is free to
     elect how harnesses are implemented and how the triple is to be provided as
     long as it is trivially possible to do so from common HTTP clients such as
     a web browser and cURL. For instance, the following Rocket route accepts
     the triple via a combination of query parameters and body data:

     ```rust
     use rocket::serde::json::Json;

     #[post("/?<harness>&<args..>", data = "<program>")]
     fn execute(harness: Harness, args: HashMap<&str, &str>, program: &str) { /* .. */ }
     ```

     An alternative is to use unique routes for each harness. This allows
     statically declaring harness arguments:

     ```rust
     #[post("/example&<arg>", data = "<stub>")]
     fn run_example(arg: ExampleArg, stub: &str) { /* .. */ }

     #[post("/mock&<method>&<uri>", data = "<stub>")]
     fn run_mock_request(method: Method, uri: Origin<'_>, stub: &str) { /* .. */ }
     ```

     **Deliverable:** A pull request which contains the updates to the
     application and two proof of concept harnesses:
       - **Example Execution:** A harness that demonstrates how the web
         application can be used to execute code examples in [Rocket's guide].
         This harness likely takes no arguments.
       - **Mock Requests:** A harness that receives source code to a Rocket
         application as well as method and URI strings. The method and URI
         strings are used to construct and dispatch a [`local`] request to the
         Rocket application corresponding to the submitted source code. The
         status and body of the response are returned.

  4. **Performance Improvements**

     Implement the three performance enhancements described in [performance].

     **Deliverable:** A pull request implementing the performance enhancements
     as well as measurements of the performance impact under ideal, worst-case,
     and average-case scenarios.

[`local`]: https://api.rocket.rs/v0.5/rocket/local/

# Compensation and Timeline
[compensation]: #compensation

The following table describes award distribution and expected timeline based on
milestone completion:

| Milestone Completed | Compensation | Running Total | Expected Duration |
|---------------------|--------------|---------------|-------------------|
| 1: Plan             | $100         | $100          | 1 week            |
| 2: Sandboxing       | $500         | $600          | 2.5 weeks         |
| 3: Harness Support  | $250         | $850          | 1.5 weeks         |
| 4: Performance      | $150         | $1000         | 1 week            |
| **Total**           | **$1000**    | ---           | **6 weeks**       |
