# Next.js Dashboard

This project was created out of curiosity and follows the Next.js dashboard application's [course curriculum](https://nextjs.org/learn).

## Notes

Unable to start the course with npm due to dependency conflicts. The only way to get started was to use pnpm.
This is my first time ever using it. I don't understand why it doesn't work with npm. The only thing I know about
pnpm is that there are packages out there that require pnpm people to do all sorts of workarounds. Other than that,
pnpm seems to be widely enjoyed.

I ran into a floating point precision issue when trying to
[store invoice amount in cents](https://nextjs.org/learn/dashboard-app/mutating-data#storing-values-in-cents).
Certain invoice amount values would prevent database mutations although no errors would be displayed and the form
seemed to have submitted successfully. I solved this by using the [decimal.js](https://github.com/MikeMcl/decimal.js#readme)
package. More info on this in `/app/lib/actions.ts`.

The best parts of this course were the topics of [partial prerendering](https://nextjs.org/learn/dashboard-app/partial-prerendering)
and performing [searching and pagination](https://nextjs.org/learn/dashboard-app/adding-search-and-pagination)
using URL search params. There was a lot of good info spread throughout the lessons though. The sections about forms
and [mutating data](https://nextjs.org/learn/dashboard-app/mutating-data) was also interesting. I've been using
[react-hook-form](https://react-hook-form.com/docs) for years now and it has been the only way I'd ever want to
handle forms. It was cool to have server-rendered forms that use uncontrolled inputs, but it seems that forms give
the best UX when marked as `"use client"` to make use of certain client hooks such as `useActionState`. I may try
sticking with react-hook-form due to this, but I'll need to see how it can be used with these newer APIs.
There is a short section in the [Authentication chapter](https://nextjs.org/learn/dashboard-app/adding-authentication#password-hashing)
that mentions how the Nextjs `middleware.ts` is incompatible with certain Nodejs APIs. This is apparently
[going to change](https://github.com/vercel/next.js/discussions/71727), but I wonder if the approach that was
used to overcome that limitation could've been used to solve an issue I was having with a previous test project.
I just sifted through the code of that project and it looks like I may have already known about this approach.
It didn't seem to work for me, but there is a _slight_ configuration difference that I never tried. In this `nextjs-dashboard`
codebase, the `auth.config.ts` has an empty `providers` array. The providers are actually setup in the `auth.ts` file.
In the previous project, I tried setting up the provider directly in the `auth.config.ts`. Perhaps this small change
was the missing piece to success 🤔.

This course contains some useful utilities and components that I may yoink for future projects, such as
the invoice page's breadcrumbs and pagination.

If I were to remake this app, I'd probably implement stuff from my other projects, as well as substitute some of the
packages, such as [shadcn/ui](https://ui.shadcn.com/) and [Lucide Icons](https://lucide.dev/icons/). I would also
separate the database from Vercel and use something like [Prisma](https://www.prisma.io/) to handle the queries.
