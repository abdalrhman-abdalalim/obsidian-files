```bash
/pages
  └── clients
      ├── index.js                    # /clients
      └── [id]
          ├── index.js               # /clients/:id
          └── [clientProjectId].js   # /clients/:id/:clientProjectId
```
### 🔗 Route Mapping Table

| File Path                           | URL Pattern                     | Description                              |
| ----------------------------------- | ------------------------------- | ---------------------------------------- |
| `clients/index.js`                  | `/clients`                      | List of all clients                      |
| `clients/[id]/index.js`             | `/clients/:id`                  | Single client page (e.g., profile)       |
| `clients/[id]/[clientProjectId].js` | `/clients/:id/:clientProjectId` | A specific project for a specific client |
### Accessing Nested Dynamic Route Params

To access both parameters (`id` and `clientProjectId`), use the `useRouter` hook:

```tsx
import { useRouter } from 'next/router';

const ClientProjectPage = () => {
  const router = useRouter();
  const { id, clientProjectId } = router.query;

  return (
    <div>
      <h1>Client ID: {id}</h1>
      <h2>Project ID: {clientProjectId}</h2>
    </div>
  );
};

export default ClientProjectPage;
```