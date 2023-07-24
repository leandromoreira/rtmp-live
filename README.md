# RTMP Live

## What is this?

This repository provides a comprehensive guide and code samples for creating a small streaming platform based on the **RTMP** (Real-Time Messaging Protocol). The platform enables live streaming capabilities and leverages NGINX RTMP for receiving video streams. Additionally, the repository includes functionality to play the recorded videos via HTTP directly from another pool of servers.

Additionally, a service discovery process is included to report the active streams to an API. The API, integrated with Redis, returns the server and manifest path required for playback.

```mermaid
graph LR
    A[Edge] -- Which server should I request video? --> B[API]
    B -- Get server --> C[Redis]
    B -- Response with Origin Server 1 --> A
    A -- Request content --> D[Origin Server 1]
    E[Origin Server 2]
```

## What's the stack behind it?

This small live streaming platform relies on the following projects:

* [`NGINX-RTMP`](https://github.com/arut/nginx-rtmp-module) - the widely, battle-tested and probably the most famous RTMP server
* [`NGINX`](https://www.nginx.com/) - the most used werb server in the world
* [`Lua`](https://www.lua.org/) - a simple yet very powerful programing language 🇧🇷
* [`Go`](https://go.dev/) - a good language to build HTTP APIs, workers, daemons and every kind of distribued system service

## Edge - CDN

The Edge server, often referred to as "the frontend server" is an essential component of the Content Delivery Network (CDN). It plays a crucial role in the media streaming platform, facilitating a seamless viewing experience for users.

It is the server delivered by the platform you are using to watch the video, this is the server your media player will use to play the video.

The Edge server serves as the intermediary between the end-users and the video content they wish to watch. When you access a video on the platform, your media player interacts with the Edge server, which efficiently delivers the video content to your device. This playable URL comes through an HTTP API and it is out of the scope of this educational project.

