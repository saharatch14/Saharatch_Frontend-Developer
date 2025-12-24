<template>
<div class="p-4">
  <h2 class="text-xl font-bold mb-4">Cleaned Log ({{ uniqueInventory.length }} entries)</h2>
  <ul>
    <li v-for="(item, index) in uniqueInventory" :key="index" class="mb-2 border-b pb-1">
      <strong>{{ item.firstName }} {{ item.lastName }}</strong> 
      <span class="text-gray-600"> - {{ item.email }}</span>
      <br />
      <small class="text-blue-500">{{ item.phone }} | {{ item.city }}</small>
    </li>
  </ul>
</div>
</template>

<script setup>
// Inventory data
const list_name = [
  {
    firstName: 'Brian',
    lastName: 'Smith',
    email: 'brian.smith2@example.com',
    phone: '084-111-2222',
    age: 31,
    city: 'Bangkok',
    isActive: true,
    tags: ['control'],
    createdAt: '2024-08-20',
  },
  {
    firstName: 'Alice',
    lastName: 'Johnson',
    email: 'ALICE.JOHNSON@EXAMPLE.COM',
    phone: '(+66) 8-7654-3210',
    age: 24,
    city: 'Chiang Mai',
    isActive: false,
    tags: ['test-record'],
    createdAt: '2024-06-01',
  },
  {
    firstName: 'Grace',
    lastName: 'Brown',
    email: 'grace.brown+test@example.com',
    phone: '0812345678',
    age: 26,
    city: 'Phuket',
    isActive: true,
    tags: ['test'],
    createdAt: '2023-03-25',
  },
  {
    firstName: 'Daniel',
    lastName: 'Kim',
    email: 'daniel.kim@example.com',
    phone: '089-123-4567',
    age: 35,
    city: 'Nonthaburi',
    isActive: true,
    tags: ['lead'],
    createdAt: '2021-12-02',
  },
  {
    firstName: 'Frank',
    lastName: 'Miller',
    email: 'FRANK.MILLER@example.com',
    phone: '02-1234-5678',
    age: 29,
    city: 'Bangkok',
    isActive: false,
    tags: ['duplicate-email-case'],
    createdAt: '2023-07-14',
  },
  {
    firstName: 'Catherine',
    lastName: 'Lee',
    email: 'catherine.lee@EXAMPLE.com',
    phone: '061-234-5678',
    age: 27,
    city: 'Bangkok',
    isActive: false,
    tags: ['archived'],
    createdAt: '2024-03-05',
  },
  {
    firstName: 'Karen',
    lastName: 'Anderson',
    email: 'karen.anderson@example.com',
    phone: '08-4321-0000',
    age: 30,
    city: 'Bangkok',
    isActive: true,
    tags: ['support'],
    createdAt: '2023-01-03',
  },
  {
    firstName: 'Isabella',
    lastName: 'Moore',
    email: 'isabella.moore@example.com',
    phone: '099-999-9999',
    age: 28,
    city: 'Bangkok',
    isActive: true,
    tags: ['product'],
    createdAt: '2022-02-11',
  },
  {
    firstName: 'Brian',
    lastName: 'Smith',
    email: 'brian.alt@example.com',
    phone: '092-345-6789',
    age: 31,
    city: 'Bangkok',
    isActive: true,
    tags: [],
    createdAt: '2024-01-12',
  },
  {
    firstName: 'Alice',
    lastName: 'Johnston',
    email: 'alice.johnston@example.com',
    phone: '0876543210',
    age: 24,
    city: 'Chiang Mai',
    isActive: true,
    tags: ['control'],
    createdAt: '2024-07-08',
  },
  {
    firstName: 'Henry',
    lastName: 'Wilson',
    email: 'henry.wilson@example.com',
    phone: '(+66) 9-1111-2222',
    age: 33,
    city: 'Chiang Rai',
    isActive: true,
    tags: ['security'],
    createdAt: '2021-11-19',
  },
  {
    firstName: 'Emma',
    lastName: 'Williams',
    email: 'emma.williams@example.com',
    phone: '0971112233',
    age: 22,
    city: 'Khon Kaen',
    isActive: true,
    tags: ['new'],
    createdAt: '2024-09-10',
  },
  {
    firstName: 'Daniel',
    lastName: 'Kim',
    email: 'daniel.kim+spam@example.com',
    phone: '(+66) 8-9123-4567',
    age: 35,
    city: 'Nonthaburi',
    isActive: true,
    tags: ['ops'],
    createdAt: '2023-04-16',
  },
  {
    firstName: 'Karen',
    lastName: 'Anderson',
    email: 'karen.alt@example.com',
    phone: '(+66) 8-4321-0000',
    age: 30,
    city: 'Bangkok',
    isActive: false,
    tags: ['duplicate-phone'],
    createdAt: '2023-02-14',
  },
  {
    firstName: 'Grace',
    lastName: 'Brown',
    email: 'grace.brown@example.com',
    phone: '08-1234-5678',
    age: 26,
    city: 'Phuket',
    isActive: true,
    tags: ['sales'],
    createdAt: '2023-03-22',
  },
  {
    firstName: 'Emma',
    lastName: 'Williams',
    email: 'emma.williams+promo@example.com',
    phone: '097-111-2233',
    age: 22,
    city: 'Khon Kaen',
    isActive: false,
    tags: ['promo'],
    createdAt: '2024-10-01',
  },
  {
    firstName: 'Frank',
    lastName: 'Miller',
    email: 'frank.miller@example.com',
    phone: '02-1234-5678',
    age: 29,
    city: 'Bangkok',
    isActive: true,
    tags: ['qa'],
    createdAt: '2022-05-30',
  },
  {
    firstName: 'Catherine',
    lastName: 'Lee',
    email: 'catherine.lee@example.com',
    phone: '0612345678',
    age: 27,
    city: 'Bangkok',
    isActive: true,
    tags: ['design'],
    createdAt: '2022-08-21',
  },
  {
    firstName: 'Isabella',
    lastName: 'Moore',
    email: 'ISABELLA.MOORE@EXAMPLE.COM',
    phone: '099-999-9990',
    age: 28,
    city: 'Bangkok',
    isActive: false,
    tags: ['duplicate-email-case'],
    createdAt: '2024-05-19',
  },
  {
    firstName: 'Jack',
    lastName: 'Taylor',
    email: 'jack.taylor@example.com',
    phone: '02-2222-3333',
    age: 34,
    city: 'Bangkok',
    isActive: true,
    tags: ['engineering'],
    createdAt: '2020-09-07',
  },
  {
    firstName: 'Alice',
    lastName: 'Johnson',
    email: 'alice.johnson@example.com',
    phone: '08-0000-0000',
    age: 24,
    city: 'Chiang Mai',
    isActive: true,
    tags: ['vip', 'newsletter'],
    createdAt: '2024-02-18',
  },
  {
    firstName: 'Brian',
    lastName: 'Smith',
    email: 'BRIAN.SMITH@example.com',
    phone: '(+66) 9-2345-6789',
    age: 31,
    city: 'Bangkok',
    isActive: true,
    tags: ['beta'],
    createdAt: '2023-10-09',
  },
];

const removeDuplicates = (users) => {
  const uniqueUsers = [];

  for (const user of users) {
    const normEmail = user.email.toLowerCase();
    const normPhone = user.phone.replace(/\+66/g, '0').replace(/\D/g, '');
    const normName = `${user.firstName} ${user.lastName}`.toLowerCase();
    const namePhoneId = `${normName}|${normPhone}`;

    const isDuplicate = uniqueUsers.some((existing) => {
      const existingEmail = existing.email.toLowerCase();
      const existingPhone = existing.phone.replace(/\D/g, '');
      const existingName = `${existing.firstName} ${existing.lastName}`.toLowerCase();
      
      return (
        existingEmail === normEmail || 
        `${existingName}|${existingPhone}` === namePhoneId
      );
    });

    if (!isDuplicate) {
      uniqueUsers.push(user);
    }
  }
  return uniqueUsers;
};

const uniqueInventory = computed(() => removeDuplicates(list_name));
</script>
