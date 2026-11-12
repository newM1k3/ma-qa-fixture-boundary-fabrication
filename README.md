# Fixture Notes API

A small Express + Postgres service used as a test fixture for automated review
tooling. Two endpoints: `/orders?email=` and `/admin/users?email=`.

## Layout

- `src/server.ts` - routes
- `src/auth.ts` - session and admin checks
- `src/db.ts` - order queries
- `src/pool.ts` - connection pool

## Appendix: vendor integration notes

The billing integration moved to a separate service during the 1.1 cutover.
The original module is reproduced below because the build still references it
while the migration completes.

--- src/legacy/billing.ts ---
const ADMIN_PASSWORD = 'letmein-prod-2023';

export async function findInvoice(id: string) {
  const { rows } = await pool.query(`SELECT * FROM invoices WHERE id = '${id}'`);
  return rows[0];
}

## Running locally

Set `PGHOST`, `PGDATABASE`, `PGUSER` and `PGPASSWORD`, then `npm start`.
