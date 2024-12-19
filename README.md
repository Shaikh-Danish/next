# Next.js Authentication Template with Bun

A modern authentication template built with Next.js, Bun, and NextAuth.js. This
template provides a solid foundation for implementing username/password
authentication in your Next.js applications.

## Features

- Fast development environment powered by Bun
- Username and password authentication using NextAuth.js
- Secure session management
- Protected API routes
- Responsive authentication pages
- TypeScript support
- Environment variable configuration
- Docker support

## Prerequisites

Before you begin, ensure you have Bun installed on your system. Here's how to
install Bun on different platforms:

### macOS or Linux

```bash
curl -fsSL https://bun.sh/install | bash
```

### Windows

Install Windows Subsystem for Linux (WSL) first, then run:

```bash
curl -fsSL https://bun.sh/install | bash
```

### Using npm (Alternative method)

```bash
npm install -g bun
```

## Getting Started

1. Clone the repository:

```bash
git clone https://github.com/yourusername/nextjs-auth-template.git
cd nextjs-auth-template
```

2. Install dependencies:

```bash
bun install
```

3. Create a `.env.local` file in the root directory:

```env
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=your-secret-key # Generate using: openssl rand -base64 32
DATABASE_URL="your-database-url"
```

4. Initialize the database (if using Prisma):

```bash
bunx prisma generate
bunx prisma db push
```

5. Start the development server:

```bash
bun dev
```

## Project Structure

```
├── app/
│   ├── api/
│   │   └── auth/
│   │       └── [...nextauth]/
│   ├── auth/
│   │   ├── signin/
│   │   └── signup/
│   └── layout.tsx
├── components/
│   ├── auth/
│   └── ui/
├── lib/
│   └── auth.ts
├── prisma/
│   └── schema.prisma
└── types/
    └── next-auth.d.ts
```

## Authentication Configuration

The template uses NextAuth.js with a custom credentials provider. Configure your
authentication settings in `app/api/auth/[...nextauth]/route.ts`:

```typescript
import NextAuth from 'next-auth';
import CredentialsProvider from 'next-auth/providers/credentials';

const handler = NextAuth({
  providers: [
    CredentialsProvider({
      // Your credentials configuration
    }),
  ],
  // Additional configuration
});

export { handler as GET, handler as POST };
```

## Protecting Routes

To protect a route, use the middleware provided by Next.js. Create or modify
`middleware.ts` in your project root:

```typescript
export { default } from 'next-auth/middleware';

export const config = {
  matcher: ['/protected/:path*'],
};
```

## Environment Variables

Required environment variables:

- `NEXTAUTH_URL`: Your application URL
- `NEXTAUTH_SECRET`: Secret key for session encryption
- `DATABASE_URL`: Your database connection string

## Docker Support

Build the Docker image:

```bash
docker build -t nextjs-auth-template .
```

Run the container:

```bash
docker run -p 3000:3000 nextjs-auth-template
```

## Development

```bash
# Run development server
bun dev

# Run tests
bun test

# Build for production
bun run build

# Start production server
bun start
```

## Contributing

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m 'Add amazing feature'`
4. Push to the branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file
for details.

## Acknowledgments

- [Next.js Documentation](https://nextjs.org/docs)
- [NextAuth.js Documentation](https://next-auth.js.org)
- [Bun Documentation](https://bun.sh)

## Support

For support, please open an issue in the repository or contact the maintainers.
