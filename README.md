This repository demonstrates how to directly interact with Unity Physics without using Unity's Entity Component System (ECS)†.

https://user-images.githubusercontent.com/12469377/144763598-822187f1-0de6-4d10-a274-b823958fbd6c.mp4

**Unity Physics** is a deterministic‡ and stateless physics engine by Unity Technologies. [You can read more about it here](https://docs.unity3d.com/Packages/com.unity.physics@0.0/manual/design.html). Although it comes packaged with prebuilt components for Unity's entity component system, the core engine is decoupled from ECS. Determinism and statelessness are very useful for networking, where consistency in physics between server and client is important.

🚨 **This project is a very minimal proof of concept**; no thought has been put into API design, completeness or performance.

† *Unity Physics does depend on the `Entity` struct itself from ECS.*

‡ *Unity Physics is described as "deterministic", but I assume this is restricted to determinism across a single platform due to inconsistencies between some floating point arithmetic between platforms (e.g. ARM vs x86).*

**Fork Changes**

- Upgraded Unity version to 2021
- Upgraded DOTS packages to 0.51
- Moved the simulation step inside a burst able job
- Simulation stepping from `FixedUpdate` instead of `Update`
- Quadrupled the number of dyanmics bodies

Quick performance check in the editor shows 350-500 fps on a Ryzen 5900x. Note that this still uses `StepImmediate`, which I think is fine and closer to how it'd run on a single core server.