---
layout: post
title:  "Game Of Life as a Way to Pass the Life"
date:   2025-03-11 23:10:00 -0500
categories: EN ComputerScience
---

## How much did I work?

Today I had some clases that in total added to 4 hours of work. After that I
didn't felt so well so I decided to spent the rest of the day in a little side
project that could lift my spirits.

## What was I working on?

I worked a little bit in some exercises for homeworks in university but the most
important thing I did was a little Conways Game of Life in Raylib. I was not fealing
great so it isn't a big or difficult project. I just wanted to feel accompplished
at the end of the day and actually I did.

## Something worty to Share?

It is really cool to work on `C` for some projects and it could be really good
to make this kind of stops in life just to make some little project that helps
you spiritualy.

It was my first time coding the game of life and it wasn't as big of a problem
working in C as I expected. The code ended up being less than 200 lines and almost
all is really simple. Just for the sake of enjoying the process let me share some
code snippets that I find really cool.

```C
int GetMinWidthHeight() {
    return (GetScreenWidth() > GetScreenHeight()) ?
    GetScreenHeight() : GetScreenWidth();
}
```

The ternary operator was something I have seen in JS and Ruby in some projects
but seeing it in C was suprising. I wrote this code after a minimum amount of
research on internet and knowing this kind of syntactic sugar is available is
really cool.

```C
int CountLiveNeighbors(enum PosibleState **game, int i, int j) {
    int LiveNeighbors = 0;
    for (int k = -1; k <= 1; k++) {
        for (int l = -1; l <= 1; l++ ) {
            int XPos = (i + k + L_CELL) % (L_CELL);
            int YPos = (j + l + L_CELL) % (L_CELL);
            if ((k != 0 || l != 0) &&
                game[XPos][YPos] == Live ||
                game[XPos][YPos] == NextDie)
                LiveNeighbors++;
        }
    }

    return LiveNeighbors;
}
```

this code is really simple and made me proude of my self. When I was writing it
I was remembering some of my first projects in Rust (I think it was the island
problem but I'm not quite sure) that I litterally hardcoded all the posible options
in a vector list and check one by one. This function is neither complex nor prize
worty but it's means a lot to me seeing how much I improve.

```C
enum PosibleState{
    Die,
    Live,
    NextLive,
    NextDie,
};
```

I was actually surprised of how well it worked this simple Idea. The problem that
worries me more when I was starting this little problem was managing how can I keep
the previous state while changing for the next step. The thing was I could make some
intermediate value that let me keep the state (If I'm changing the State NextLive
is equivalent to Die and NextDie is the same as Live) and that way when I ended
the changes I could simply apply it and live my life. I made the iteration twice
but this code was thinked for like $$25x25$$ cells and I have already iterate
over this cells multiple times before so neither I cared one more iteration or
worried me about taking in consideration I would need to slow down my code for
greater appreciation later. This implementation has also the benefit of not needing
any more space than the simple game state. That way there was less posibilities of
memory leaks.

There it is, some of the cool things I think was worty to share about my work today.
If you want to look at the code I made is in the github Repo that I link just.
down below. Hope you like it.

## Cool Links?

* [Conway's Game Of Life](https://github.com/S1e7J/RayLib-Game-Of-Life)
* [Explanation of GOL](https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life)
