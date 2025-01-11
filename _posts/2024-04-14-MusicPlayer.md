---
title: "Music-Player [Project]"
description: "Want to build a music player? This blog covers a C++ implementation with a linked list playlist, featuring shuffle, play, pause, and more with the code on GitHub."
date: 2024-04-14 00:00:00 +0000
categories: [Project, C++]
tags: [Project, C++, DSA]
image: 
    path: assets/img/misc/musicplayer.jpeg
    alt: Just a Vibing Linux Penguin
---

# Music Player in C++: A Simple Command-Line Music Player

Welcome to a detailed guide on creating a simple command-line music player in C++! This program allows you to queue and play songs from your playlist, as well as control playback with several features such as next, previous, pause, resume, shuffle, and stop. 

The code is available on GitHub: [Music-Player](https://github.com/paulrounak/Music-Player.git).

> **Note:** This project is designed specifically for Linux systems.
{: .prompt-info }

## Features

The music player provides the following functionalities:

- **Queue Music**: Add songs to the playlist.
- **Play Music**: Start playing songs from the queue.
- **Next Music**: Skip to the next song in the queue.
- **Previous Music**: Go back to the previous song in the queue.
- **Pause Music**: Pause the currently playing song.
- **Resume Music**: Resume the paused song.
- **Shuffle Music**: Play a random song from the queue.
- **Stop Music**: Stop the current song and exit the program.

## The Code

### Queue Music (`queueMusic` method)
The `queueMusic` function adds a song to the music queue while avoiding duplicates.

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
- **Checking for duplicates**: Traverses the queue to ensure the song is not already in the list.
- **Adding the song**: Creates a new `musicQueue` node and updates the `head`, `tail`, `next`, and `prev` pointers.

### Play Music (`playMusic` method)
The `playMusic` function plays songs from the queue, starting with the first.

```cpp
void MusicPlayer::playMusic() {
    if (head == nullptr) {
        cout << "No music in queue" << endl;
    } else {
        for (curr = head; curr != nullptr; curr = curr->next) {
            cout << "Playing " << curr->music << endl;
            system(("mpg123 -q " + MusicDir + "/" + curr->music + " &").c_str());
            // Menu options for controlling playback
        }
    }
}
```

**Explanation:**
- **Play the song**: Uses `system()` to invoke the `mpg123` command for playback.
- **Menu controls**: Displays playback options for the user.

### Next Music (`case 1` in `playMusic`)
Allows the user to skip to the next song.

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
- **Check for next song**: Verifies if there is a next song in the queue.
- **Play next song**: Updates `curr` to the next song and starts playback.

### Previous Music (`case 2` in `playMusic`)
Allows the user to go back to the previous song.

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
- **Check for previous song**: Ensures the user is not at the start of the queue.
- **Play previous song**: Updates `curr` to the previous song and resumes playback.

### Pause and Resume Music (`case 3` and `case 4`)
Controls to pause and resume playback.

```cpp
case 3:  // Pause
    system("pkill -STOP mpg123");
    break;
case 4:  // Resume
    system("pkill -CONT mpg123");
    break;
```

**Explanation:**
- **Pause**: Sends a stop signal to the `mpg123` process.
- **Resume**: Sends a continue signal to `mpg123`.

### Shuffle Music (`case 5`)
Plays a random song from the queue.

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
- **Randomize the queue**: Selects a random song by traversing the queue `n` times.
- **Play random song**: Resumes playback with the selected song.

### Stop Music (`case 6`)
Stops playback and exits the program.

```cpp
case 6:
    system("pkill mpg123");
    exit(0);
    break;
```

**Explanation:**
- **Stop playback**: Terminates the `mpg123` process.
- **Exit**: Ends the program execution.

## Installation and Usage

To use this music player, follow these steps:

1. **Clone the repository:**
   ```bash
   git clone https://github.com/paulrounak/Music-Player.git
   ```

2. **Compile the code:**
   ```bash
   g++ main.cpp
   ```

3. **Run the program:**
   ```bash
   ./a.out
   ```

## Conclusion
This C++ music player offers an interactive way to manage a playlist via a command-line interface. By using a doubly linked list for efficient queue management and `mpg123` for music playback, it provides a simple yet powerful tool to enjoy your favorite songs. Try it out and have fun listening!
