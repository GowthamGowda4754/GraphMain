GRAPHMIND + FALKORDB INTEGRATION PATCH

Copy these files into the root of your existing GraphMind project, preserving paths:
- package.json                         (replace existing)
- vite.config.ts                       (replace existing)
- .env.example                         (reference only; do not overwrite a real .env)
- server/falkordbServer.ts              (replace existing)

Then, in the project root terminal:
1) npm install --legacy-peer-deps
2) Create a file named .env in the project root (same folder as package.json).
3) Add the FALKORDB_* values from your FalkorDB Cloud connection details.
   Use the hostname only in FALKORDB_HOST, the port in FALKORDB_PORT, the database password in
   FALKORDB_PASSWORD, and set FALKORDB_TLS=true if the provider requires TLS (common for cloud).
4) Start backend in terminal 1: npm run server
5) Start frontend in terminal 2: npm run dev
6) Test backend: curl http://localhost:3001/api/status
   A working connection returns status "connected" and connected: true.
7) Open http://localhost:3000. Vite now proxies /api requests to port 3001.

Notes:
- This patch makes /api/graph/query execute real Cypher queries against FalkorDB. The rest of the
  app's memory/project CRUD is still currently handled by the frontend's local store unless its
  service methods are separately migrated to backend endpoints.
- Do not deploy this API publicly until proper server-side authentication/authorization and query
  restrictions are implemented. The existing demo token check is not production-grade.
- Keep .env private; never paste the password into chat or commit it to GitHub.
