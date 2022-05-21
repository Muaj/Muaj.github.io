---
layout: post
title: Top Down Game
subtitle: First time experimenting with Unity
cover-img: /assets/img/diary.jpg
thumbnail-img: /assets/img/diary.jpg
share-img: /assets/img/diary.jpg
tags: [unity, game]
---

My goal with this project is to familiarize myself with Unitys environment and see how it feels like to develop and design a game from scratch. Im particularly interested rogue-likes and with my limited knowledge and resources I decided to make a 16-bit game with rogue-like systems, although I haven't fully decided on what kind of combat or environment this game would take place in. This is my very first Dev Diary.

## Player Movement

<iframe width="560" height="315" src="https://www.youtube.com/embed/0frdkTuw8Qc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Simple character movement

```c#
hit = Physics2D.BoxCast(transform.position, boxCollider.size, 0, new Vector2(0, moveDelta.y), Mathf.Abs(moveDelta.y * Time.deltaTime), LayerMask.GetMask("Actor", "Blocking"));
        if (hit.collider == null)
        {
            //Movement
            transform.Translate(0, (moveDelta.y * Time.deltaTime) * 3, 0);
        }

        hit = Physics2D.BoxCast(transform.position, boxCollider.size, 0, new Vector2(moveDelta.x, 0), Mathf.Abs(moveDelta.x * Time.deltaTime), LayerMask.GetMask("Actor", "Blocking"));
        if (hit.collider == null)
        {
            //Movement
            transform.Translate((moveDelta.x * Time.deltaTime) * 3, 0, 0);
        }
```

This is the code that causes character movement. While the character is moving extremely slowly in the video you can change the speed in which the character moves by changing this 3 value to one higher.

```c#
transform.Translate(0, (moveDelta.y * Time.deltaTime) * 3, 0);
transform.Translate((moveDelta.x * Time.deltaTime) * 3, 0, 0);
```

## Player Collision

<iframe width="560" height="315" src="https://www.youtube.com/embed/y_CZnSn5qOY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

I've added the ability for the player to collide with mobs, while the mob in the video is a slime I plan to allow characters to phase through these, while being forced to collide with boss type mobs.

```c#
//Checks if we can move in this direction by casting a box there first
//if box returns null, we can move there
hit = Physics2D.BoxCast(transform.position, boxCollider.size, 0, new Vector2(0, moveDelta.y), Mathf.Abs(moveDelta.y _ Time.deltaTime), LayerMask.GetMask("Actor", "Blocking"));
if (hit.collider == null)
{
//Movement
transform.Translate(0, (moveDelta.y _ Time.deltaTime) \* 5, 0);
}

        hit = Physics2D.BoxCast(transform.position, boxCollider.size, 0, new Vector2(moveDelta.x, 0), Mathf.Abs(moveDelta.x * Time.deltaTime), LayerMask.GetMask("Actor", "Blocking"));
        if (hit.collider == null)
        {
            //Movement
            transform.Translate((moveDelta.x * Time.deltaTime) * 5, 0, 0);
        }
```

The player unit projects its hitbox forwards and when it runs into the hitbox of the slime it returns 'actor' instead of null. This result fails the check required to move causing the two sprites to collide.

## Perlin Noise Map

I'm currently experimenting with using perlin noise to generate my map tiles.
