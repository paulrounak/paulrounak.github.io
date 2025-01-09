---
title: "Music-Player [Project]"
description: "Want to build a music player? This blog covers a C++ implementation with a linked list playlist, featuring shuffle, play, pause, and more with the code on GitHub."
date: 2024-04-14 00:00:00 +0000
categories: [Project, C++]
tags: [Project, C++]
image: 
    path: assets/img/misc/musicplayer.jpeg
    alt: Just a Vibing Linux Penguin
---


# Music Player in C++: A Simple Command-Line Music Player 

Welcome to a detailed guide on creating a simple command-line music player in C++! This program allows you to queue and play songs from your playlist, as well as control playback with several features such as next, previous, pause, resume, shuffle, and stop. Let’s walk through the code and understand how the different features work.

The code is available on GitHub: [Music-Player](https://github.com/paulrounak/Music-Player.git).

## Features 

The music player provides the following functionalities:
 
- **Queue Music** : Add songs to the playlist.
 
- **Play Music** : Start playing the songs in the queue.
 
- **Next Music** : Skip to the next song in the queue.
 
- **Previous Music** : Go back to the previous song in the queue.
 
- **Pause Music** : Pause the currently playing song.
 
- **Resume Music** : Resume the paused song.
 
- **Shuffle Music** : Play a random song from the queue.
 
- **Stop Music** : Stop the current song and exit the program.

## The Code 

Let's dive into the code and understand each part in detail.
**Queue Music**  (`queueMusic` method)The `queueMusic` function adds a song to the music queue. It checks if the song already exists in the queue to avoid duplicates.
  


```cpp
void MusicPlayer::queueMusic(string music) {
    if (head != nullptr) {
        for (curr = head; curr != nullptr; curr = curr->next) {
            if (curr->music == music) {
                cout << "Music already in queue" << endl;
                return;
            }
        }
    }

    curr = new musicQueue;
    curr->music = music;
    curr->next = nullptr;
    curr->prev = nullptr;
    if (head == nullptr) {
        head = curr;
        tail = curr;
    } else {
        tail->next = curr;
        curr->prev = tail;
        tail = curr;
    }
}
```

 **Explanation:** 
 
- **Checking for duplicates** : Before adding a song to the queue, the code checks if it already exists in the list by traversing the queue. If the song is found, it prints "Music already in queue" and does not add it again.
 
- **Adding the song** : If the song is unique, a new `musicQueue` node is created, and the song is added to the queue by updating the `head`, `tail`, `next`, and `prev` pointers accordingly.


---

**Play Music**  (`playMusic` method)

The `playMusic` function plays the songs in the queue one by one, starting from the head of the queue. It also offers a menu to control the playback.
  


```cpp
void MusicPlayer::playMusic() {
    if (head == nullptr) {
        cout << "No music in queue" << endl;
    } else {
        for (curr = head; curr != nullptr; curr = curr->next) {
            cout << "Playing " << curr->music << endl;
            system(("mpg123 -q " + MusicDir + "/" + curr->music + " &").c_str());
            // Menu options for controlling playback
            // Choice handling (Next, Previous, Pause, Resume, Shuffle, Stop)
        }
    }
}
```

 **Explanation:** 
 
- **Play the song** : If the queue is not empty, the program starts by playing the first song using `system()` to invoke the `mpg123` command.
 
- **Menu for controls** : After each song is played, the user is prompted with a menu to control playback (next, previous, pause, etc.). The user can make a choice to navigate through the queue or manipulate playback.


---

**Next Music**  (`case 1` in `playMusic`)

The "Next" option allows the user to skip to the next song in the queue.

  


```cpp
case 1:
    if (curr->next == nullptr) {
        cout << "No next music" << endl;
    } else {
        curr = curr->next;
        cout << "Playing " << curr->music << endl;
        system("pkill mpg123");
        system(("mpg123 -q " + MusicDir + "/" + curr->music + " &").c_str());
    }
    break;
```

 **Explanation:** 
 
- **Check for next song** : The code checks if there is a next song available in the queue by inspecting `curr->next`. If there is no next song, it notifies the user.
 
- **Play the next song** : If a next song exists, the program updates `curr` to point to the next song and restarts the `mpg123` player to play the new song.


---

**Previous Music**  (`case 2` in `playMusic`)

The "Previous" feature allows the user to go back to the previous song in the queue.

  


```cpp
case 2:
    if (curr->prev == nullptr) {
        cout << "No previous music" << endl;
    } else {
        curr = curr->prev;
        cout << "Playing " << curr->music << endl;
        system("pkill mpg123");
        system(("mpg123 -q " + MusicDir + "/" + curr->music + " &").c_str());
    }
    break;
```

 **Explanation:** 
 
- **Check for previous song** : The code checks if there is a previous song by looking at `curr->prev`. If the user is at the beginning of the queue, it notifies the user that there is no previous song.
 
- **Play the previous song** : If a previous song exists, the program updates `curr` to point to the previous song and restarts the music using `mpg123`.


---

**Pause and Resume Music**  (`case 3` and `case 4`)

The "Pause" and "Resume" options allow the user to pause and resume the playback.

  


```cpp
case 3:  // Pause
    system("pkill -STOP mpg123");
    break;
case 4:  // Resume
    system("pkill -CONT mpg123");
    break;
```

 **Explanation:** 
 
- **Pause** : The `pkill -STOP mpg123` command sends a stop signal to the `mpg123` process, pausing the music.
 
- **Resume** : The `pkill -CONT mpg123` command sends a continue signal to `mpg123`, resuming the music where it left off.


---

**Shuffle Music**  (`case 5`)

The "Shuffle" option allows the user to play a random song from the queue.

  


```cpp
case 5:  // Shuffle
    for (int i = 0; i < n; i++) {
        if (curr->next == nullptr) {
            curr = head;
        } else {
            curr = curr->next;
        }
    }
    cout << "Playing " << curr->music << endl;
    system("pkill mpg123");
    system(("mpg123 -q " + MusicDir + "/" + curr->music + " &").c_str());
    break;
```

 **Explanation:** 
 
- **Randomize the queue** : The program generates a random number `n` and traverses the queue `n` times, moving to the next song each time. If it reaches the end, it loops back to the head of the queue.
 
- **Play the randomized song** : After determining a random song, it is played using `mpg123`.


---

**Stop Music**  (`case 6`)

The "Stop" feature stops the current music and exits the program.

  


```cpp
case 6:
    system("pkill mpg123");
    exit(0);
    break;
```

 **Explanation:** 
 
- **Stop the music** : The `pkill mpg123` command is used to kill the `mpg123` process, stopping the current song immediately.
 
- **Exit the program** : After stopping the music, the program exits using `exit(0)`.


---


## Installation and Usage 

To get started with this music player, follow these installation steps:
 
1. **Clone the repository** :

```bash
git clone https://github.com/paulrounak/Music-Player.git
```
 
2. **Compile the code** :

```bash
g++ main.cpp
```
 
3. **Run the program** :

```bash
./a.out
```

Once the program is running, you can:

- Add songs to the queue.

- Play music.

- Control playback with options like next, previous, pause, resume, shuffle, and stop.


---


## Conclusion 
This C++ music player provides an easy and interactive way to manage a playlist using a simple command-line interface. The program leverages a doubly linked list to handle the queue efficiently, and the use of system calls with `mpg123` enables music playback directly in the terminal. Try it out, add your favorite songs, and enjoy the music!
