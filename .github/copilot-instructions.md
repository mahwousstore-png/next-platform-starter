# GitHub Copilot Instructions for next-platform-starter

## Project Overview
This is a full-stack employee expenses management platform built with React 19, TypeScript, Vite, Express, and Supabase. The application manages employee custody balances and expense tracking with Arabic language support.

## Architecture
- **Client**: React SPA in `client/` directory, built with Vite
- **Server**: Express.js API in `server/` directory, bundled with esbuild
- **Shared**: Common types/constants in `shared/` directory
- **Expenses Feature**: Separate React app in `expenses/` directory for expense management
- **Backend**: Supabase with PostgreSQL, RLS policies for employees/expenses tables
- **Deployment**: Netlify (SPA routing, static file serving)

## Key Components & Data Flow
- **Expense Types**: `work_expense` (negative, deducts from custody), `custody_payment` (positive, adds to custody), `salary`, `bonus`, `deduction`, `loan`, `other`
- **Balance Logic**: Expenses automatically update employee `custodyBalance` - positive amounts add to balance, negative amounts deduct
- **Status Flow**: `pending` → `paid` (employee confirmation) or `rejected`
- **Auth**: Supabase auth with user roles (`admin`, `user`, `owner`) stored in `raw_app_meta_data`

## Development Workflow
- **Package Manager**: pnpm (see `pnpm-lock.yaml`)
- **Build Commands**:
  - `pnpm dev` - Start Vite dev server on port 3000
  - `pnpm build` - Build client to `dist/public` and server to `dist/index.js`
  - `pnpm start` - Run production server from `dist/index.js`
  - `pnpm check` - TypeScript type checking
  - `pnpm lint` - ESLint with custom rules
  - `pnpm format` - Prettier formatting
- **Testing**: No test framework configured yet
- **Environment**: Uses `.env` files for Supabase config (`VITE_SUPABASE_URL`, `VITE_SUPABASE_ANON_KEY`)

## Code Patterns & Conventions
- **Imports**: Path aliases - `@/` for `client/src/`, `@shared` for `shared/`
- **UI Components**: shadcn/ui with "new-york" style, CSS variables, Tailwind CSS
- **State Management**: Local storage for data persistence (currently mock implementation)
- **Forms**: React Hook Form with Zod validation
- **Styling**: Tailwind with custom CSS variables in `client/src/index.css`
- **Language**: Arabic text throughout UI (`تسجيل مصروف`, `المبلغ`, etc.)
- **Error Handling**: Toast notifications with `sonner`
- **Routing**: Wouter for client-side routing
- **Icons**: Lucide React icons

## Expense Management Logic
- **Amount Handling**: User enters positive amounts, system applies negative sign for deductions based on `EXPENSE_TYPES`
- **Balance Updates**: Automatic calculation in `dataService.updateEmployeeBalance()`
- **Confirmation Flow**: Employees confirm receipt of payments, admins manage all operations
- **Transaction Reversal**: Delete operations reverse balance effects

## File Structure Examples
```
client/src/
├── components/
│   ├── ui/           # shadcn/ui components
│   └── expenses/     # Expense-specific components
├── lib/
│   ├── data-service.ts  # Local storage operations
│   └── supabase.ts     # Supabase client setup
├── pages/           # Route components
├── types/           # TypeScript definitions
└── contexts/        # React contexts (Theme, etc.)
```

## Integration Points
- **Supabase RLS**: Policies ensure employees see only their expenses, admins see all
- **External Integration**: `inject-expense-btn.js` injects expense buttons into other systems
- **OAuth**: Portal authentication via `getLoginUrl()` in `const.ts`

## Common Tasks
- **Add Expense Type**: Update `EXPENSE_TYPES` in `types/index.ts` and handle logic in `data-service.ts`
- **UI Components**: Use `npx shadcn@latest add [component]` to add new shadcn/ui components
- **Database Changes**: Add migrations in `supabase/migrations/`
- **Environment Setup**: Configure Supabase project and update environment variables

## ESLint Rules
- `@typescript-eslint/no-explicit-any`: off (flexible typing allowed)
- `@typescript-eslint/no-unused-vars`: error with `_` prefix ignored
- `react/no-unescaped-entities`: off (Arabic text contains entities)
- Special rules for `ManusDialog.tsx` and `usePersistFn.ts`

## Deployment Notes
- **Netlify**: Builds with `vite build`, serves from `dist/public`
- **SPA Routing**: All routes redirect to `index.html`
- **Server**: Express serves static files and handles API routes (currently minimal)