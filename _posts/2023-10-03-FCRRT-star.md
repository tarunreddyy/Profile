---
title: Flight-cost Rapidly-exploring Random Tree Star (FCRRT*)
author: Tarun Trilokesh
layout: post
---

## Summary of the topic in layman’s terms:

In today's bustling cities, skyscrapers paint the skyline, vehicles thrum on the roads below, and people, engrossed in their daily routines, navigate the labyrinth of urban life. Now, imagine a bird's-eye view of this intricate tapestry. From such a height, the city appears like an elaborate maze, with its winding roads, towering buildings, and bustling hubs of activity.

But what if, instead of birds, we have drones buzzing above, trying to find their way amidst this urban jungle? These aren't your typical drones, taking casual flights. They have missions – be it delivering a package, capturing aerial footage of an event, or conducting a rapid survey. These drones require a sophisticated "brain" or system to help them navigate efficiently, ensuring they don't collide with buildings, conserve their battery, and reach their destinations swiftly.

This is where the Flight Cost RRT* (FC-RRT*) comes into play.

Imagine you're playing a video game where you have to move a character through a maze. You'd be constantly calculating and recalculating the best routes, trying to avoid obstacles and dead-ends. FC-RRT* does something very similar, but for drones in real-life urban environments. Think of it as a super-smart GPS system, designed exclusively for these flying machines. But it's not just any GPS; it's like having a seasoned cab driver who knows every alley, shortcut, and street of a city and continually updates the route based on traffic, road closures, or other unforeseen challenges.

The "Rapidly-exploring Random Trees" or RRT aspect of the algorithm is akin to the drone casting a wide net of possible paths, exploring all potential routes it can take. It's like plotting various routes on a map. But the "Star" in RRT* signifies an added layer of intelligence. The drone doesn't just find a way; it keeps refining and optimizing it. So, if a quicker or safer path becomes apparent, the drone adjusts its course.

The "Flight Cost" component takes this a step further. It's not just about finding the quickest route, but also the most energy-efficient one. Much like how we, when driving, might opt for a slightly longer route if it means smoother roads and less fuel consumption, drones equipped with FC-RRT* consider the energy or battery usage for each potential path. This ensures they don't just reach their destination quickly, but also with enough battery reserve, making their missions more successful and reliable.

To put it in even simpler terms, let's consider a relatable analogy. Imagine you're in a vast library, looking for a specific book. You have a vague idea of where it might be, so you start exploring. As you walk through the aisles, you begin to piece together a clearer path, avoiding sections you know don't contain your book. Along the way, you keep refining your search strategy, ensuring you're not wasting time or energy. The FC-RRT* algorithm is like your search strategy, guiding the drone, ensuring it doesn't waste its battery, and gets to its destination efficiently.

In essence, the FC-RRT* algorithm is the behind-the-scenes hero for drones, ensuring they navigate the intricate dance of urban environments seamlessly. It's the bridge between the digital intelligence of machines and the practical demands of the real world, ensuring our skies are safe, and drones are efficient.


## Formal definition using appropriate notation

The FC-RRT* algorithm is fundamentally rooted in the principles of the Rapidly-exploring Random Trees (RRT*), enhanced to consider the flight costs or energy consumption when determining paths for drones. Here's a detailed breakdown of its formal definition and mechanics:

### 1. **Defining the Workspace**:

Let's start by defining our workspace. This is the environment or area where our drone operates.

- **S**: Represents the complete workspace, including both free and obstructed spaces.
- **S_{free}**: Denotes the subset of **S** that's free from obstacles, essentially the navigable space.


### 2. **Tree Growth and Sampling**:

The core principle of RRT* is to grow a tree that represents possible paths.

- \( x_{init} \): The starting point or the initial position of the drone.
- \( x_{rand} \): A randomly sampled point within \( S_{free} \). This serves as a potential new node for our tree.

### 3. **Connecting the Nodes**:

The tree grows by connecting these nodes, taking into consideration the shortest and most efficient routes.

- \( x_{nearest} \): For a given \( x_{rand} \), this represents the nearest node already in our tree.
- \( x_{new} \): A new node created by extending the tree from \( x_{nearest} \) towards \( x_{rand} \).

Using these notations, the basic process of tree expansion in RRT* can be represented as:


$$ x_{new} = \text{extend}(x_{nearest}, x_{rand}) $$


Where the function "extend" represents the operation of growing the tree towards a new point.

### 4. **Path Optimization**:

The "Star" in RRT* signifies continuous refinement. Once \( x_{new} \) is added:

- We inspect all nodes in a vicinity of \( x_{new} \) to see if connecting through \( x_{new} \) offers a shorter path.
- If a shorter path is identified, the tree is reconnected to utilize \( x_{new} \) as a waypoint.

This can be mathematically represented by:

\[
$$ \text{if } C(x_{near}, x_{goal}) > C(x_{new}, x_{goal}) + C(x_{near}, x_{new}) $$
\]

Where \( C \) is the cost function, \( x_{near} \) is a neighboring node, and \( x_{goal} \) is our destination. If the above condition is true, the path from \( x_{near} \) to \( x_{goal} \) via \( x_{new} \) is shorter, and the tree is reconnected accordingly.

### 5. **Incorporating Flight Cost**:

The fundamental enhancement in FC-RRT* is the introduction of a flight cost component. Instead of just distance, the cost function \( C \) also considers energy or battery consumption. This ensures the paths aren't just short, but also energy efficient.

\[
C(x_1, x_2) = \alpha \times \text{distance}(x_1, x_2) + \beta \times \text{energy\_cost}(x_1, x_2)
\]

Here, \( \alpha \) and \( \beta \) are weights, allowing us to balance between raw distance and energy consumption. The function "distance" calculates the spatial distance between two points, while "energy\_cost" evaluates the energy consumption between the two points.
