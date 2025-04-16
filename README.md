# Video Streaming Backend

This is the backend service for a video streaming application. It provides RESTful APIs for uploading, streaming, and serving videos, including support for HLS (HTTP Live Streaming).

## Features

- **Video Upload**: Upload videos with metadata (title and description).
- **Retrieve Videos**: Fetch all uploaded videos.
- **Stream Videos**: Stream videos directly or in chunks.
- **HLS Support**: Serve HLS playlists (`master.m3u8`) and video segments (`.ts` files).

## Endpoints

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
- **Path Variable**:
  - `videoId` (String): The ID of the video to stream.
- **Response**: Video file as a `Resource`.

---

### 4. Stream Video in Chunks
- **URL**: `/api/v1/videos/stream/range/{videoId}`
- **Method**: `GET`
- **Description**: Stream a video in chunks using the `Range` header.
- **Path Variable**:
  - `videoId` (String): The ID of the video to stream.
- **Request Header**:
  - `Range` (String): The byte range to stream.
- **Response**: Partial video file as a `Resource`.

---

### 5. Serve HLS Master Playlist
- **URL**: `/api/v1/videos/{videoId}/master.m3u8`
- **Method**: `GET`
- **Description**: Serve the HLS master playlist file for a video.
- **Path Variable**:
  - `videoId` (String): The ID of the video.
- **Response**: HLS master playlist file as a `Resource`.

---

### 6. Serve HLS Video Segments
- **URL**: `/api/v1/videos/{videoId}/{segment}.ts`
- **Method**: `GET`
- **Description**: Serve individual HLS video segments.
- **Path Variables**:
  - `videoId` (String): The ID of the video.
  - `segment` (String): The segment name.
- **Response**: HLS video segment file as a `Resource`.

## Configuration

- **HLS Directory**: The directory for storing HLS files is configured using the `file.video.hsl` property in the `application.properties` file.
- **Chunk Size**: The chunk size for video streaming is defined in [`AppConstants`](src/main/java/com/stream/app/AppConstants.java).

## Dependencies

- **Spring Boot**: For building the REST API.
- **Lombok**: For reducing boilerplate code.
- **MultipartFile**: For handling file uploads.
- **FileSystemResource**: For serving files from the file system.
- **MediaType**: For setting content types in responses.

## Notes

- Ensure the `HLS_DIR` property is correctly set in the `application.properties` file.
- The `Range` header is required for chunked video streaming.
- The controller uses `UUID` to generate unique IDs for videos.

---

## Project Structure

- **Controllers**: Handles API requests (e.g., `VideoController`).
- **Entities**: Defines database models (e.g., `Video`, `Course`).
- **Services**: Contains business logic (e.g., `VideoService`).
- **Payloads**: Custom response messages (e.g., `CustomMessage`).

---

## Technologies Used

- **Spring Boot**: Backend framework.
- **Lombok**: Reduces boilerplate code.
- **JPA**: For database interactions.
- **HLS**: For adaptive video streaming.

---

## How to Run

1. Clone the repository.
2. Configure the `application.properties` file with the required properties.
3. Build and run the application using:
   ```bash
   mvn spring-boot:run
