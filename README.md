This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/app/api-reference/cli/create-next-app).

## Getting Started

Node.js 24.22.2 is included in `.tools/`. From the project root, run:

```bash
PATH="$PWD/.tools/bin:$PATH" npm run dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

## BMAD Method

BMAD Method v6.12.4 is installed in `_bmad/`, with its Codex skills in `.agents/skills/`. The local `uv` executable and managed Python 3.11 are in `.tools/`.

When running BMAD workflows from a terminal, make the project tools available first:

```bash
export PATH="$PWD/.tools/bin:$PATH"
export UV_PYTHON_INSTALL_DIR="$PWD/.tools/python"
```

Then start Codex from this project folder and invoke the `bmad-help` skill to choose a workflow.

## Supabase

The Supabase project URL and publishable key are configured in the local `.env.local` file using `NEXT_PUBLIC_SUPABASE_URL` and `NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY`. Copy `.env.example` to `.env.local` when setting up another environment, then add the URL and publishable key from the Supabase project's API settings. The local file is ignored by Git. Restart the development server after changing environment variables. The client helpers fail with a configuration error if either variable is missing.

Use `src/lib/supabase/client.ts` in Client Components and `src/lib/supabase/server.ts` in Server Components, Server Actions, or Route Handlers. In Server Components, use the server client for reads; cookie writes are available from Server Actions and Route Handlers. Supabase queries return errors in their `error` field, which callers should handle.

`proxy.ts` refreshes Auth sessions for matched application requests (including `/api` routes) and skips common static assets. This refresh does not protect routes or authorize database access: verify user claims where access control is needed and use Supabase Row Level Security policies for data. Narrow the matcher if a future route should not refresh sessions. Only the publishable key is used; never put a Supabase secret or service-role key in a `NEXT_PUBLIC_` variable.

You can start editing the page by modifying `src/app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/app/building-your-application/optimizing/fonts) to automatically optimize and load [Geist](https://vercel.com/font), a new font family for Vercel.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/app/building-your-application/deploying) for more details.
