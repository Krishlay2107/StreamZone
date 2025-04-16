# Video Streaming Application

This project is a full-stack video streaming application that allows users to upload, retrieve, and stream videos. It supports adaptive streaming using HLS (HTTP Live Streaming).

---

## Features

### Backend
- **Video Upload**: Upload videos with metadata (title and description).
- **Retrieve Videos**: Fetch all uploaded videos.
- **Stream Videos**: Stream videos directly or in chunks.
- **HLS Support**: Serve HLS playlists (`master.m3u8`) and video segments (`.ts` files).

### Frontend
- **Video Playback**: Play videos using HLS with adaptive streaming.
- **Video Upload**: Upload videos with a user-friendly interface.
- **Responsive Design**: Video player adapts to different screen sizes.
- **Error Handling**: Displays error messages for unsupported formats.

---

## Backend Endpoints

### 1. Upload Video
- **URL**: `/api/v1/videos`
- **Method**: `POST`
- **Description**: Upload a video file along with its metadata.
- **Request Parameters**:
  - `file` (MultipartFile): The video file to upload.
  - `title` (String): The title of the video.
  - `description` (String): The description of the video.
- **Response**:
  - `200 OK`: Video uploaded successfully.
  - `500 Internal Server Error`: Video upload failed.

---

### 2. Get All Videos
- **URL**: `/api/v1/videos`
- **Method**: `GET`
- **Description**: Retrieve a list of all uploaded videos.
- **Response**: List of `Video` objects.

---

### 3. Stream Video
- **URL**: `/api/v1/videos/stream/{videoId}`
- **Method**: `GET`
- **Description**: Stream a video by its ID.
- **Response**: Video file as a `Resource`.

---

### 4. Stream Video in Chunks
- **URL**: `/api/v1/videos/stream/range/{videoId}`
- **Method**: `GET`
- **Description**: Stream a video in chunks using the `Range` header.
- **Response**: Partial video file as a `Resource`.

---

### 5. Serve HLS Master Playlist
- **URL**: `/api/v1/videos/{videoId}/master.m3u8`
- **Method**: `GET`
- **Description**: Serve the HLS master playlist file for a video.
- **Response**: HLS master playlist file as a `Resource`.

---

### 6. Serve HLS Video Segments
- **URL**: `/api/v1/videos/{videoId}/{segment}.ts`
- **Method**: `GET`
- **Description**: Serve individual HLS video segments.
- **Response**: HLS video segment file as a `Resource`.

---

## Frontend Components

### 1. `VideoPlayer.jsx`
- A React component for video playback.
- **Features**:
  - HLS support using `hls.js`.
  - Fallback for native HLS playback in compatible browsers.
  - Error handling for unsupported video formats.

---

### 2. `VideoUpload.jsx`
- A React component for uploading videos.
- **Features**:
  - File upload with metadata (title and description).
  - Progress bar for upload status.
  - Success and error notifications using `react-hot-toast`.

---

## Configuration

### Backend
- **HLS Directory**: Set in `application.properties` using the `file.video.hsl` property.
- **Chunk Size**: Defined in `AppConstants`.

### Frontend
- **Video Source**: Pass the HLS playlist URL (`master.m3u8`) to the `VideoPlayer` component.

---

## Technologies Used

### Backend
- **Spring Boot**: REST API development.
- **Lombok**: Reduces boilerplate code.
- **JPA**: Database interactions.
- **HLS**: Adaptive video streaming.

### Frontend
- **React**: User interface.
- **Video.js** and **HLS.js**: Video playback.
- **Flowbite**: UI components for forms and buttons.

---

## How to Run

### Backend
1. Clone the repository.
2. Configure the `application.properties` file with the required properties.
3. Build and run the application using:
   ```bash
   mvn spring-boot:run
