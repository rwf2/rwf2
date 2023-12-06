# User Stories

The RWF2 is actively interested in partnering with Rocket's users to highlight
the framework's unique strengths and capabilities through _user stories_. The
goal is not only to attract new users but also bolster the confidence of
existing users by examining specific real-world experiences. By sharing your
experience with Rocket, you simultaneously contribute to the foundation's cause
while exposing your company or project to a wide and eager audience.

## Overview

User stories are written documents, typically ranging from 1 to 3 letter pages
in length, that describe specific real-world development experiences with
Rocket. They generally follow the structure of offering background information
on the project or company, articulating relevant technical challenges, and
explaining how Rocket helped address them, with emphasis on any of Rocket's
distinctive features that were of particular importance.

User stories may be as detailed or general as you'd like. They may be written in
the third-person about specific challenges and their solutions or be
first-person accounts that provide a broader perspective. They can provide
in-depth, data-driven analyses of particular problems and their solutions with
Rocket, or they can share a broader anecdotal narrative, showcasing a particular
use of Rocket and/or its impact on software development.

Ultimately, the goal is to disseminate your unique experiences with Rocket in
whichever form available. If you've had a positive experience with Rocket, we
want you to share it and are more than happy to collaborate with you to discover
the best approach to doing so.

## Proposed Outline

While there's no specific formula to follow when writing a user story, we
propose the following outline as a guideline.

  * **Introduction**: A brief introduction to the project, product, and/or
    company, as well as the problems that resulted in seeking a solution
    ultimately solved with Rocket.

  * **Challenges with Existing Approaches**: What motivated the use of Rocket
    specifically, and if alternatives were considered or replaced, why they
    weren't up to the task.

  * **Results with Rocket**: The positive effects of using Rocket, typically
    with data to back-up claims.

  * **Key Insights**: Expands on the specific features of Rocket
    leveraged to achieve the results.

  * **Conclusion**: Concludes by reemphasizing the problems and how Rocket has
    helped solve them.

## A Fictional Example

The following is a fictional example of a user story that follows the proposed
outline. Given its fictional nature, it is missing details from reality that
would lead to a more compelling story. Use this example as a guideline only.

#### Introduction

Comet develops and deploys IoT devices engineered to integrate seamlessly
with daily life in space, providing astronauts with immediate access to
critical statistics. Comet's devices deliver real-time data from sensors
around the spacecraft, requiring continuous connectivity.

In the demanding environment of space, every millisecond is crucial. Achieving
high performance coupled with the required reliability was a significant
challenge. When astronauts began reporting issues with device responsiveness and
inconsistencies in data, the Comet engineering team knew it was time to rewrite
the backing Python-based web servers. Comet chose Rocket. With Rocket, the Comet
engineering team has seen a dramatic decrease in resource utilization and
hardware costs, and uptime increased from a respectable 98% to an incredible
100%.

#### Challenges with Existing Approaches

Prior to the adoption of Rocket, the Comet engineering team encountered
substantial challenges with their Python-based web servers—the backbone of
their IoT devices. These servers often struggled under heavy loads, with
latency spikes of up to 800 milliseconds during peak activity. Resource
utilization also posed ongoing concerns; servers frequently operated at 75%
of CPU capacity and used excessive memory, leading to occasional downtime
and maintenance hurdles.

> *Our previous Python servers were like outdated rocket boosters struggling
> to keep up with the new age of space travel. The shift to Rocket was like
> upgrading to a hyper-efficient engine.*
>
> Marcus Reid, Senior Software Architect, Comet

#### Results with Rocket

[graph of latency before Rocket / after Rocket]

After careful research, the Comet engineering team transitioned their web server
infrastructure to Rocket. This transformation had a profound impact.
Post-implementation, average latency was reduced from 500 milliseconds to 30
milliseconds, while CPU usage fell to an efficient 15%. Memory consumption was
cut to just 10% of previous levels, resulting in a leaner, more stable operating
environment. Thanks to these improvements, the team was able to switch to
lighter hardware, reducing hardware costs by 50% while simultaneously increasing
device responsiveness.

#### Key Insights

The benefits gained from the implementation of Rocket extend beyond
performance metrics. Security and robustness are critical. Rocket allows the
Comet engineering team to enforce strict access controls and precisely
validate incoming requests at all times. Guard transparency allows security
engineers to establish clear and concise security protocols which all other
engineers are _required_ to adhere to.

> *Implementing Rocket's request guards with guard transparency was a
> game-changer. It's like having an elite security team working 24/7 to
> protect our application.*
>
> Ethan Choi, Head of Security, Comet

Specifically, Comet tasks their security team with writing security-sensitive
guards; the backend team can then use those guards without being concerned about
their implementation. By leveraging request-guard transparency, the security
team can also _ensure_ that request guards are used whenever they should be.
This separation of policy concern was something the Comet software engineering
team had been searching for but failed to find prior to Rocket. This
security-first approach, integrated into the core of the web server code,
ensures that the devices remain secure and operational.

#### Conclusion

The strategic decision by the Comet engineering team to rewrite their Python web
servers with Rocket has proven to be pivotal in their mission to deliver robust
devices for space use. By leveraging Rocket and its advanced features, they have
not only seen a remarkable decrease in latency and resource utilization but also
halved their hardware costs. The centralized policy enforcement via request
guards has bolstered confidence among the engineering staff.

> *The move to Rocket wasn't just an upgrade; it was a necessary evolution
> to keep pace with the demands of space technology. It has set a new
> standard for our engineering practices and product offerings.*
>
> Emily White, Chief Technology Officer, Comet

Comet's experience is a compelling example of how the right technology can
address current challenges and drive a company towards a more successful future.

## Real-World Examples

We highlight a few examples of other organizations' user story analogs below.

  * We think [OpenAI's customer stories](https://openai.com/customer-stories)
    serve as overall great examples:

    * https://openai.com/customer-stories/duolingo
    * https://openai.com/customer-stories/khan-academy
    * https://openai.com/customer-stories/ironclad

  * This Rust case study on NPM is a good example of the general structure:

    * https://www.rust-lang.org/static/pdfs/Rust-npm-Whitepaper.pdf

  * Cloudflare's case studies demonstrate a good challenge/solution structure:

    * https://www.cloudflare.com/case-studies/genuine-parts-company/
    * https://www.cloudflare.com/case-studies/polestar/
    * https://www.cloudflare.com/case-studies/sage/

  * Datadog's case studies include "Key Results" that are valuable metrics:

    * https://www.datadoghq.com/case-studies/deliveryhero/
    * https://www.datadoghq.com/case-studies/compass/
