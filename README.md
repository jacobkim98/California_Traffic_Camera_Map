# California Traffic Camera Map

Red Light & Speed Camera 위치를 Google Maps에 표시하는 웹앱입니다.

## Demo

🔗 [Live Demo](https://california-traffic-camera-map.vercel.app)

## Features

- **카메라 위치 표시**: 캘리포니아 내 단속 카메라를 지도에 마커로 표시
  - 🔴 Red Light Camera (빨간색)
  - 🟠 Speed Camera (주황색)
  - 🔵 User Reported (파란 테두리)

- **사용자 제보 기능**: 새로운 카메라 위치 추가 가능
- **삭제 기능**: 잘못된 제보 삭제 가능
- **실시간 동기화**: Supabase를 통한 데이터 저장

## Tech Stack

| Area | Technology |
|------|------------|
| Frontend | HTML, CSS, JavaScript |
| Map | Google Maps JavaScript API |
| Data Source | OpenStreetMap (Overpass API) |
| Backend | Supabase (PostgreSQL) |
| Deployment | Vercel |

## Data Flow

```
OpenStreetMap → 초기 카메라 데이터 (51개)
       ↓
Google Maps API → 지도에 마커 표시
       ↓
Supabase ← 사용자 제보 저장/조회/삭제
```

## Getting Started

### Prerequisites

- Google Maps API Key
- Supabase Account & Project

### Setup

1. Clone the repository
```bash
git clone https://github.com/jacobkim98/California_Traffic_Camera_Map.git
```

2. Update API keys in `index.html`
```javascript
const SUPABASE_URL = 'your-supabase-url';
const SUPABASE_KEY = 'your-supabase-anon-key';
```

3. Create Supabase table
```sql
create table cameras (
  id bigint primary key generated always as identity,
  lat double precision not null,
  lng double precision not null,
  type text not null default 'speed',
  created_at timestamp with time zone default now()
);

alter table cameras enable row level security;
create policy "Anyone can read" on cameras for select using (true);
create policy "Anyone can insert" on cameras for insert with check (true);
create policy "Anyone can delete" on cameras for delete using (true);
```

4. Open `index.html` in browser or deploy to Vercel

## Future Improvements

- 전 미국으로 확대 (5,000+ 카메라)
- 모바일 앱 (백그라운드 알림)
- 경로 기반 카메라 경고
- 사용자 인증

## License

MIT

## Built With

🤖 Built with [Claude Code](https://claude.ai/code) - Vibe Coding
