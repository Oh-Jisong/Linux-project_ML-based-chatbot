<p align="center">
  <h1 align="center">Emotion-Based Music Recommendation Chatbot</h1>
</p>

<p align="center">
  PHP · Docker · MariaDB · Chart.js 기반 감정 분석 음악 추천 웹 서비스
</p>

<p align="center">
  <img src="https://img.shields.io/badge/PHP-8.x-blue">
  <img src="https://img.shields.io/badge/Docker-Compose-informational">
  <img src="https://img.shields.io/badge/DB-MariaDB-orange">
  <img src="https://img.shields.io/badge/Status-Active-success">
</p>

---

## Project Overview

본 프로젝트는 사용자가 입력한 상황 설명 텍스트를 기반으로  
사전 정의된 감정 분류 규칙을 적용하여,  
해당 감정에 맞는 음악 플레이리스트를 자동 추천하는 **웹 기반 챗봇 서비스**입니다.

Docker 기반 환경에서 PHP 웹 서버와 MariaDB를 분리 구성하여  
실제 서비스 배포 구조와 유사한 형태로 시스템을 설계하였으며,  
감정 기록 저장, 통계 시각화, 로그인 세션 관리까지 포함한 **풀스택 구조 실습 프로젝트**입니다.

---

## Why This Project

단순 챗봇 구현을 넘어,  
실제 웹 서비스 형태로 사용자 입력 → 처리 로직 → DB 저장 → 시각화 → 추천 결과 제공까지  
전체 데이터 흐름을 직접 설계하고 구현하는 것을 목표로 진행했습니다.

특히 서버 환경 구성, 컨테이너 기반 배포 구조, 세션 인증,  
데이터베이스 설계 경험을 동시에 확보하는 것을 중점으로 개발했습니다.

---

## Technical Highlights

| Area | Description |
------|------
**Service Architecture** | Docker Compose 기반 PHP · MariaDB · phpMyAdmin 멀티 컨테이너 구성  
**Authentication** | PHP Session 기반 로그인 / 회원가입 시스템 구현  
**Data Storage** | 사용자 대화 기록 및 감정 로그 영속 저장  
**Rule-based NLP Logic** | 키워드 매칭 기반 감정 분류 및 검색어 자동 매핑  
**Visualization** | Chart.js 기반 감정 통계 대시보드 구현  
**External Access Test** | ngrok + QR 코드 기반 모바일 외부 접속 테스트  

---

## System Architecture

- **Web Server**: PHP + Apache  
- **Database**: MariaDB  
- **Container Orchestration**: Docker Compose  
- **Visualization**: Chart.js  
- **Admin Tool**: phpMyAdmin  

---

## Emotion Classification Logic

본 시스템은 AI 모델 대신  
사전 정의된 키워드 매칭 규칙 기반으로 감정을 분류합니다.

| Emotion | Example Keywords | YouTube Search Query |
--------|----------------|-------------------
분노 | 화나, 짜증, 빡쳐 | 화났을 때 듣는 노래 플레이리스트  
슬픔 | 우울, 슬퍼, 눈물 | 우울할 때 듣는 노래 플레이리스트  
외로움 | 외로워, 혼자, 쓸쓸 | 외로울 때 듣는 노래 플레이리스트  
불안 | 불안, 초조, 긴장 | 불안할 때 듣는 노래 플레이리스트  
걱정 | 걱정돼, 고민 | 걱정될 때 듣는 노래 플레이리스트  
사랑 | 사랑해, 설레 | 사랑에 빠졌을 때 듣는 노래 플레이리스트  
기쁨 | 행복해, 신나 | 신나는 노래 플레이리스트  

---

## Database Schema

### users

| Column | Type | Description |
-------|------|------------
id | VARCHAR | User ID (PK)  
nickname | VARCHAR | Display Name  
password | VARCHAR | Hashed Password  

### chat_history

| Column | Type | Description |
-------|------|------------
id | INT (AI) | Primary Key  
user_id | VARCHAR | FK → users  
event | TEXT | User Input Text  
emotion | VARCHAR | Classified Emotion  
youtube_link | TEXT | Generated Playlist Link  
created_at | DATETIME | Timestamp  

---

## Project Structure

```bash
.
├── db/                 # MariaDB initialization scripts
├── web/                # PHP web application
├── images/             # UI screenshots
├── docker-compose.yml
└── README.md
```

---

## Getting Started

### 1. Clone Repository
```bash
git clone https://github.com/OhJisong/Linix-project_Rule-based-chatbot.git
cd Linix-project_Rule-based-chatbot
```

### 2. Run Docker Containers
```bash
docker-compose up --build
```

### 3. Access Web Service
```bash
http://localhost:8080
```

**phpmyadmin**
```bash
http://localhost:8081
```

---

## What I Learned

Docker Compose 기반 멀티 컨테이너 웹 서비스 구성 경험

PHP 세션 기반 인증 시스템 구현

감정 로그 데이터 저장 및 통계 시각화 파이프라인 구축

Rule-based 텍스트 처리 로직 설계

실제 서비스 흐름에 가까운 웹 애플리케이션 구조 설계

---

## Future Improvements

REST API 구조로 백엔드 분리

OAuth 기반 소셜 로그인 연동

AI 기반 감정 분류 모델 적용

추천 결과 개인화 알고리즘 고도화

서비스 로그 및 사용자 행동 분석 기능 추가

---

## Note

본 프로젝트는 학습 목적의 웹 서비스 실습 프로젝트이며,
실제 배포 환경과 유사한 구조 설계 및 데이터 흐름 구현을 목표로 개발되었습니다.
