# k6 script template

```javascript
import http from 'k6/http';
import { check, sleep } from 'k6';

export const options = {
  stages: [
    { duration: '30s', target: 20 },   // ramp up
    { duration: '2m', target: 20 },    // hold
    { duration: '30s', target: 100 },  // step up
    { duration: '2m', target: 100 },   // hold
    { duration: '30s', target: 0 },    // ramp down
  ],
  thresholds: {
    http_req_duration: ['p(95)<500'], // p95 latency under 500ms
    http_req_failed: ['rate<0.01'],   // error rate under 1%
  },
};

export default function () {
  const res = http.get('https://api.example.com/endpoint');
  check(res, { 'status is 200': (r) => r.status === 200 });
  sleep(1); // think time between requests, models real user pacing
}
```

Run with: `k6 run script.js`

For multi-step flows (login → browse → checkout), chain requests within the default function, passing tokens/cookies between them, rather than testing endpoints in isolation — isolated endpoint tests miss session-state-related bottlenecks (e.g. session store contention) that only show up in realistic flows.
