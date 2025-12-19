# next-platform-starter

A full-stack employee expenses management platform built with React 19, TypeScript, Vite, Express, and Supabase. The application manages employee custody balances and expense tracking with Arabic language support.

## Features

- **Employee Expense Management**: Track and manage employee expenses with different types (work expenses, custody payments, salary, bonus, deductions, loans, etc.)
- **Balance Tracking**: Automatic calculation of employee custody balances based on expense transactions
- **Role-Based Access**: Different user roles (admin, user, owner) with appropriate permissions
- **Arabic Language Support**: UI fully supports Arabic text and RTL layout
- **Real-time Updates**: Live balance updates and transaction tracking
- **Responsive Design**: Mobile-friendly interface using Tailwind CSS and shadcn/ui components
- **Secure Authentication**: Supabase authentication with Row Level Security (RLS) policies

## Tech Stack

### Frontend
- **React 19** - Modern React with latest features
- **TypeScript** - Type-safe JavaScript
- **Vite** - Fast build tool and dev server
- **Tailwind CSS** - Utility-first CSS framework
- **shadcn/ui** - High-quality UI components
- **Wouter** - Lightweight client-side router
- **React Hook Form + Zod** - Form handling with validation
- **Sonner** - Toast notifications

### Backend
- **Express.js** - Node.js web framework
- **Supabase** - PostgreSQL database with real-time features
- **esbuild** - Fast JavaScript bundler

### Development Tools
- **ESLint** - Code linting
- **Prettier** - Code formatting
- **pnpm** - Fast package manager

## Project Structure

```
next-platform-starter/
├── client/                 # React SPA
│   ├── public/            # Static assets
│   └── src/
│       ├── components/    # Reusable UI components
│       │   ├── ui/       # shadcn/ui components
│       │   └── expenses/ # Expense-specific components
│       ├── lib/          # Utilities and services
│       ├── pages/        # Route components
│       ├── types/        # TypeScript definitions
│       └── contexts/     # React contexts
├── server/                # Express.js API server
├── shared/                # Shared types and constants
├── expenses/              # Separate expense management app
├── supabase/              # Database migrations
└── dist/                  # Build output
```

## Installation

### Prerequisites
- Node.js 18+
- pnpm
- Supabase account

### Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/mahwousstore-png/next-platform-starter.git
   cd next-platform-starter
   ```

2. **Install dependencies**
   ```bash
   pnpm install
   ```

3. **Environment Setup**
   Create `.env` file in the root directory:
   ```env
   VITE_SUPABASE_URL=your_supabase_url
   VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
   ```

4. **Database Setup**
   - Create a new Supabase project
   - Run the migrations in `supabase/migrations/`
   - Configure RLS policies for employees and expenses tables

## Development

### Available Scripts

```bash
# Start development server (port 3000)
pnpm dev

# Build for production
pnpm build

# Run production server
pnpm start

# Type checking
pnpm check

# Linting
pnpm lint

# Formatting
pnpm format

# Preview production build
pnpm preview
```

### Development Workflow

1. **Start the dev server**: `pnpm dev`
2. **Open browser**: Navigate to `http://localhost:3000`
3. **Make changes**: Hot reload enabled
4. **Check code quality**: Run `pnpm lint` and `pnpm check`

## Expense Types

The system supports the following expense types:

- `work_expense` - Deducts from custody balance
- `custody_payment` - Adds to custody balance
- `salary` - Salary payments
- `bonus` - Bonus payments
- `deduction` - Deductions from balance
- `loan` - Loan transactions
- `other` - Miscellaneous expenses

## API Endpoints

### Server Routes
- `GET /api/health` - Health check
- `GET /api/expenses` - Get expenses (with RLS)
- `POST /api/expenses` - Create expense
- `PUT /api/expenses/:id` - Update expense
- `DELETE /api/expenses/:id` - Delete expense

## Deployment

### Netlify Deployment

1. **Build Settings**:
   - Build command: `pnpm build`
   - Publish directory: `dist/public`

2. **Environment Variables**:
   Set the same environment variables as in development

3. **SPA Routing**:
   Configure redirects for client-side routing

### Manual Deployment

```bash
# Build the application
pnpm build

# Start production server
pnpm start
```

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit changes: `git commit -am 'Add new feature'`
4. Push to branch: `git push origin feature/your-feature`
5. Submit a pull request

### Code Standards

- Use TypeScript for all new code
- Follow ESLint rules
- Use Prettier for formatting
- Write meaningful commit messages
- Add tests for new features

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

For support and questions:
- Create an issue on GitHub
- Check the documentation in `.github/copilot-instructions.md`

## Roadmap

- [ ] Add testing framework (Jest/Vitest)
- [ ] Implement real-time notifications
- [ ] Add expense categories and tags
- [ ] Mobile app development
- [ ] Advanced reporting and analytics
- [ ] Multi-language support beyond Arabic
