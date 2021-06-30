<template>
  <table class="table">
    <thead class="thead-dark">
      <tr>
        <th scope="col">
          #
        </th>
        <th scope="col">
          Category
        </th>
        <th scope="col">
          Name
        </th>
        <th scope="col" width="300">
          操作
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="restaurant in restaurants" :key="restaurant.id">
        <th scope="row">
          {{ restaurant.id }}
        </th>
        <td>{{ restaurant.Category ? restaurant.Category.name : '未分類' }}</td>
        <td>{{ restaurant.name }}</td>
        <td class="d-flex justify-content-between">
          <router-link
            :to="{ name: 'admin-restaurant', params: { id: restaurant.id } }"
            class="btn btn-link"
          >
            Show
          </router-link>

          <router-link
            :to="{
              name: 'admin-restaurant-edit',
              params: { id: restaurant.id }
            }"
            class="btn btn-link"
            >Edit</router-link
          >

          <button
            type="button"
            class="btn btn-link"
            @click.stop.prevent="deleteRestaurant(restaurant.id)"
          >
            Delete
          </button>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
const dummyData = {
  restaurants: [
    {
      id: 1,
      name: 'Nichole Jakubowski',
      tel: '1-148-000-8754',
      address: '536 Howe Path',
      opening_hours: '08:00',
      description: 'magnam',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=70.08628840266901',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 5,
      Category: {
        id: 5,
        name: '素食料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 2,
      name: 'Murl Balistreri',
      tel: '(376) 769-0191',
      address: '505 Daisy Cliffs',
      opening_hours: '08:00',
      description:
        'Cum molestias accusantium temporibus voluptatem voluptatem dignissimos qui odit dolorem.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=19.800869589513127',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 4,
      Category: {
        id: 4,
        name: '墨西哥料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 3,
      name: 'Maximillia Witting',
      tel: '1-976-918-4597 x5935',
      address: '190 Ledner Walks',
      opening_hours: '08:00',
      description: 'non consequatur earum',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=14.307984613043168',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 2,
      Category: {
        id: 2,
        name: '日本料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 4,
      name: 'Dr. Roderick Boehm',
      tel: '131-415-3685 x996',
      address: '738 Vivianne Expressway',
      opening_hours: '08:00',
      description: 'laudantium quasi qui',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=23.021511086514714',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 3,
      Category: {
        id: 3,
        name: '義大利料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 5,
      name: 'Niko Boehm',
      tel: '357.729.9702 x34145',
      address: '8860 Emmerich Light',
      opening_hours: '08:00',
      description: 'sunt',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=69.79427373391044',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 4,
      Category: {
        id: 4,
        name: '墨西哥料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 6,
      name: 'Adriana Robel',
      tel: '(365) 446-5105 x1662',
      address: '5607 Schumm Lights',
      opening_hours: '08:00',
      description:
        'Ea qui labore debitis voluptatum blanditiis et voluptatem ad ullam. Non suscipit consectetur est accusamus reiciendis blanditiis et quidem. Culpa sequi animi laboriosam aut.\n \rLaborum atque voluptatem tenetur qui autem ex velit dolor. Praesentium consectetur ut earum. Quis voluptatum sed laborum temporibus quibusdam nihil sint perferendis. Laudantium dolor nemo eum quibusdam quia fugit est quia sequi. Provident voluptas et saepe iure vero itaque dolore neque. Accusamus delectus quas iure ullam inventore rerum maiores aut.\n \rOdio earum accusantium consequatur deserunt omnis sit. Ab quibusdam earum. Vel aut modi dolorem nemo. Sed doloribus quaerat delectus. Aut ducimus corrupti dolor itaque deleniti sed rerum.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=24.454417695685436',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 2,
      Category: {
        id: 2,
        name: '日本料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 7,
      name: 'Mrs. Mohamed Metz',
      tel: '(313) 887-1218',
      address: '75063 Ryan Place',
      opening_hours: '08:00',
      description: 'qui',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=44.45945046298001',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 3,
      Category: {
        id: 3,
        name: '義大利料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 8,
      name: 'Lulu Schiller',
      tel: '492-807-3873 x616',
      address: '865 Lebsack Square',
      opening_hours: '08:00',
      description: 'vel',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=93.06184090927051',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 3,
      Category: {
        id: 3,
        name: '義大利料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 9,
      name: 'Yasmine Gorczany',
      tel: '323-327-7256 x0364',
      address: '389 Bins Locks',
      opening_hours: '08:00',
      description:
        'Vitae minus corporis qui. Quasi qui aut. Repellat doloribus et repellat ipsum perferendis et qui.\n \rError facere enim sequi et reprehenderit eos. Laborum aperiam in dolores et corrupti quisquam vel porro ipsam. Architecto illum est non corporis minus.\n \rSed autem eum earum soluta possimus qui. Ut illum dignissimos repellendus doloribus. Culpa nulla dolorem omnis.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=8.189480667229777',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 4,
      Category: {
        id: 4,
        name: '墨西哥料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 10,
      name: 'Izabella Corwin',
      tel: '1-336-728-0021 x96672',
      address: '4248 Raynor Highway',
      opening_hours: '08:00',
      description:
        'Consectetur rerum magnam ipsam quia aut dolor facere omnis aut.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=6.0911267309345485',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 1,
      Category: {
        id: 1,
        name: '中式料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 11,
      name: "Paris O'Kon",
      tel: '994.326.6607 x142',
      address: '37065 Zulauf Knolls',
      opening_hours: '08:00',
      description: 'corporis',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=40.995101668944',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 2,
      Category: {
        id: 2,
        name: '日本料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 12,
      name: 'Greyson Gutkowski',
      tel: '477.941.7779 x7317',
      address: '982 Lynch Shore',
      opening_hours: '08:00',
      description: 'Voluptatem reprehenderit ut.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=15.921765239261653',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 3,
      Category: {
        id: 3,
        name: '義大利料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 13,
      name: 'Miss Beulah Padberg',
      tel: '1-867-390-0716 x410',
      address: '663 Dusty Burg',
      opening_hours: '08:00',
      description: 'Veniam odio aut et nisi quidem.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=2.5724492854948267',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 3,
      Category: {
        id: 3,
        name: '義大利料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 14,
      name: 'Emerson Huel',
      tel: '357.186.9729 x129',
      address: '6698 Robel Extensions',
      opening_hours: '08:00',
      description: 'Inventore sit odit.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=93.12867665130395',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 4,
      Category: {
        id: 4,
        name: '墨西哥料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 15,
      name: 'Chelsie Terry',
      tel: '847-977-2009 x44202',
      address: '010 Crooks Cliff',
      opening_hours: '08:00',
      description: 'Voluptatum molestiae illum dolores praesentium.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=42.82366366843784',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 2,
      Category: {
        id: 2,
        name: '日本料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 16,
      name: 'Amara Simonis Sr.',
      tel: '514.187.2579 x046',
      address: '26478 Watson Lights',
      opening_hours: '08:00',
      description:
        'Sed aut esse et voluptatem. Esse fuga minima et adipisci rem.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=58.255978347657454',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 1,
      Category: {
        id: 1,
        name: '中式料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 17,
      name: 'Jaunita Ratke',
      tel: '048.716.7247 x6365',
      address: '8434 Bruen Viaduct',
      opening_hours: '08:00',
      description:
        'Ea et repellat est architecto.\nEst et ipsa officia error maxime aperiam tempore aut aut.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=97.43297648835234',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 3,
      Category: {
        id: 3,
        name: '義大利料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 18,
      name: 'Miss Collin Thiel',
      tel: '225.662.6865',
      address: '2200 Waters Stream',
      opening_hours: '08:00',
      description: 'sunt debitis officiis',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=76.57252951421493',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 5,
      Category: {
        id: 5,
        name: '素食料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 19,
      name: "Ms. Marianne O'Kon",
      tel: '342-576-1841 x786',
      address: '6310 Rolfson Land',
      opening_hours: '08:00',
      description:
        'Voluptatem aspernatur praesentium rerum aperiam deserunt ratione maxime et deleniti.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=81.50547666413136',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 4,
      Category: {
        id: 4,
        name: '墨西哥料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 20,
      name: 'Paxton Reichel',
      tel: '358.128.4942 x073',
      address: '462 Jerad Roads',
      opening_hours: '08:00',
      description: 'Sit quia ab.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=93.4573354217935',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 1,
      Category: {
        id: 1,
        name: '中式料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 21,
      name: 'Franz Fritsch',
      tel: '(508) 251-2603 x243',
      address: '31615 Dickens Court',
      opening_hours: '08:00',
      description: 'Iusto itaque incidunt corporis atque ut beatae illum modi.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=48.747999215822134',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 4,
      Category: {
        id: 4,
        name: '墨西哥料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 22,
      name: 'Jalen Wiza',
      tel: '(481) 733-1196 x002',
      address: '5201 Huels Crescent',
      opening_hours: '08:00',
      description: 'provident',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=14.37641312779736',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 3,
      Category: {
        id: 3,
        name: '義大利料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 23,
      name: 'Hadley Hyatt',
      tel: '443.486.3173 x0674',
      address: '448 Erica Ferry',
      opening_hours: '08:00',
      description:
        'Nam quas omnis qui debitis est adipisci consequatur iste.\nRecusandae aut impedit nihil repellendus molestiae.\nId rerum dolores sint et.\nConsequatur eius aliquid asperiores suscipit ipsum et in vel.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=78.34094290134476',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 4,
      Category: {
        id: 4,
        name: '墨西哥料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 24,
      name: 'Eldridge Gottlieb',
      tel: '617.436.5888',
      address: '41002 Shania Turnpike',
      opening_hours: '08:00',
      description:
        'Consequuntur voluptatem dicta molestias eum voluptas sit. Pariatur aperiam quis accusantium quo amet fuga nemo. Voluptatem dolor numquam. Veritatis reprehenderit tempore. Maxime eum omnis assumenda qui pariatur ea ex est voluptas.\n \rDebitis non ut natus. Officiis aut iure impedit cum sit ad ullam. Voluptatem dolorem et. Modi laboriosam illum ratione reprehenderit.\n \rVoluptas ad quia. Omnis dolore harum quia deleniti molestiae dolor repellat ut. Provident architecto voluptatum natus vel et.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=91.65962466098333',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 3,
      Category: {
        id: 3,
        name: '義大利料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 25,
      name: 'Elvie Treutel',
      tel: '1-559-532-4961',
      address: '27930 Moore Trafficway',
      opening_hours: '08:00',
      description: 'Rerum ducimus quas perferendis voluptas repellendus.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=55.5447949949174',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 5,
      Category: {
        id: 5,
        name: '素食料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 26,
      name: 'Mrs. Urban Goyette',
      tel: '861-467-6593',
      address: '53458 McDermott Station',
      opening_hours: '08:00',
      description:
        'Autem magni accusamus est doloremque corporis esse eveniet facilis.\nSaepe consequatur minima quaerat.\nPlaceat accusantium rerum omnis.\nRepellat aut quo dicta ut non sunt qui quam.\nMaxime dolor omnis at qui odio.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=81.53664755547234',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 1,
      Category: {
        id: 1,
        name: '中式料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 27,
      name: 'Margarett Kertzmann',
      tel: '804.832.3806',
      address: '4595 Koch Land',
      opening_hours: '08:00',
      description:
        'Optio a laudantium quia alias voluptatum hic enim. Voluptas id sed accusamus neque debitis unde accusamus. Quod doloribus voluptate omnis. Id deleniti esse in ipsam. Quam deleniti velit qui veniam et similique consectetur ea.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=95.84059771070773',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 5,
      Category: {
        id: 5,
        name: '素食料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 28,
      name: 'Anibal Ward MD',
      tel: '388-570-8072 x368',
      address: '83701 Mraz Junction',
      opening_hours: '08:00',
      description:
        'Aliquam itaque maxime voluptatem sit. Quam quas omnis odio. Voluptas dignissimos eligendi neque debitis exercitationem porro molestiae et quia.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=82.72179180585233',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 2,
      Category: {
        id: 2,
        name: '日本料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 29,
      name: 'Christian Ferry',
      tel: '(629) 934-5814 x3797',
      address: '94046 Leda Road',
      opening_hours: '08:00',
      description: 'ducimus',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=8.35678568036693',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 3,
      Category: {
        id: 3,
        name: '義大利料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 30,
      name: 'Bettye Ondricka I',
      tel: '1-318-294-4715 x364',
      address: '713 Joaquin Groves',
      opening_hours: '08:00',
      description: 'ut',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=92.39384673696891',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 4,
      Category: {
        id: 4,
        name: '墨西哥料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 31,
      name: 'Natalia Leuschke',
      tel: '(388) 470-3372 x82633',
      address: '97777 Ledner Road',
      opening_hours: '08:00',
      description:
        'Exercitationem amet asperiores maxime perspiciatis eos.\nCorporis placeat explicabo aut sit quibusdam amet est.\nEt consequatur nihil vitae expedita vel facere perferendis.\nRatione et necessitatibus harum dolores et.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=26.288593183232244',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 3,
      Category: {
        id: 3,
        name: '義大利料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 32,
      name: 'Annabel Fahey',
      tel: '168.796.2249',
      address: '3690 Rogahn Locks',
      opening_hours: '08:00',
      description:
        'Quo sit et veritatis maxime qui sed quos quis possimus.\nSed magnam eaque ex quidem.\nVoluptas ut impedit cum illo sunt.\nNemo placeat voluptatem maxime magnam labore aut repudiandae.\nOmnis vitae dicta dolores quos.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=67.04115305767601',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 5,
      Category: {
        id: 5,
        name: '素食料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 33,
      name: 'Amy Nitzsche',
      tel: '617.141.5062',
      address: '4407 Susanna Streets',
      opening_hours: '08:00',
      description:
        'Ut est sit qui voluptates sint distinctio. Quis fugit quaerat iusto ratione optio consequuntur. Esse doloribus eos suscipit ut quibusdam aliquam culpa aut. Ipsam fuga perspiciatis doloribus enim tempora. Dolore eos ipsam.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=76.52882012324278',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 4,
      Category: {
        id: 4,
        name: '墨西哥料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 34,
      name: 'Ivory Bogisich PhD',
      tel: '1-716-612-3275 x235',
      address: '1982 Carli Prairie',
      opening_hours: '08:00',
      description: 'doloribus excepturi qui',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=73.83194803056207',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 1,
      Category: {
        id: 1,
        name: '中式料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 35,
      name: 'Janet Crooks',
      tel: '1-336-294-3305 x2764',
      address: '48478 Farrell Vista',
      opening_hours: '08:00',
      description: 'ut porro sed',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=70.00390424070577',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 5,
      Category: {
        id: 5,
        name: '素食料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 36,
      name: 'Dina Kreiger',
      tel: '824.480.2115 x0622',
      address: '8745 Alberto Fords',
      opening_hours: '08:00',
      description:
        'Quos neque hic voluptates. Dolore aut impedit in exercitationem. Adipisci magni nulla. Non temporibus ullam totam sit est vel sit veritatis.\n \rVeritatis iusto repellat aut repellat error ea ut debitis. Qui totam voluptates quia quibusdam odit dolores similique fugit itaque. Placeat tenetur voluptate autem maiores excepturi quam non omnis laudantium.\n \rEt deleniti sint consequatur. Ut atque nihil tenetur nihil fugiat ut. Laudantium distinctio explicabo necessitatibus. Et sint vel eligendi in eos quo sunt repellat.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=79.30036377225656',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 3,
      Category: {
        id: 3,
        name: '義大利料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 37,
      name: 'Walter Leuschke PhD',
      tel: '(538) 861-5365',
      address: '1319 Emmerich Views',
      opening_hours: '08:00',
      description: 'possimus neque sit',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=75.54323085254511',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 1,
      Category: {
        id: 1,
        name: '中式料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 38,
      name: 'Flavie Boyer',
      tel: '(988) 746-8843 x5306',
      address: '685 Antonietta Lock',
      opening_hours: '08:00',
      description: 'ut rerum est',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=69.56608874244831',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 2,
      Category: {
        id: 2,
        name: '日本料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 39,
      name: 'Lou Howe DDS',
      tel: '(005) 898-3430 x62679',
      address: '755 Gaetano Lane',
      opening_hours: '08:00',
      description:
        'Rerum cupiditate aut. Eum sunt magni iste enim a esse et et ut. Reprehenderit praesentium impedit ipsam quis et doloremque quo quia qui. Cum sunt est nulla. Ex impedit eveniet nihil minus perferendis porro dicta.\n \rAb saepe rerum autem beatae rerum fugit ad possimus. Eum rem consequuntur velit et minima debitis molestiae autem. Corporis alias autem consequatur animi eum architecto sed non quia. Commodi ipsum ipsum distinctio soluta in suscipit quis.\n \rQuas corrupti aliquam doloribus recusandae. Dolorem eos omnis vitae quaerat blanditiis est. Tempore officia alias voluptatem sed et amet qui tempora. Ut et perferendis eos.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=14.209397715660987',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 1,
      Category: {
        id: 1,
        name: '中式料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 40,
      name: 'Kennith Leffler',
      tel: '1-927-110-8762',
      address: '40287 Buford Stream',
      opening_hours: '08:00',
      description: 'dicta',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=39.793054132212745',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 4,
      Category: {
        id: 4,
        name: '墨西哥料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 41,
      name: 'Rene Kovacek',
      tel: '1-409-838-7015 x79888',
      address: '19884 Amalia Squares',
      opening_hours: '08:00',
      description:
        'Odio doloribus distinctio perspiciatis excepturi ut mollitia autem.\nExpedita voluptatibus laboriosam sunt.\nVoluptates sint aut ad ullam aut explicabo.\nEt quibusdam facere iure.\nDeleniti fugiat itaque.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=47.71075084828254',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 4,
      Category: {
        id: 4,
        name: '墨西哥料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 42,
      name: 'Robbie Mueller',
      tel: '(950) 579-8900 x906',
      address: '09117 Bins Drive',
      opening_hours: '08:00',
      description:
        'Omnis dolore aut minima et et blanditiis optio. Sunt corrupti enim sunt saepe possimus quia quod voluptate. Optio qui et sed. Et deleniti molestiae. Minima explicabo est quos. Eum quos natus repellendus porro nisi perferendis tenetur.\n \rEum et corporis inventore ea aliquam consequatur. Est voluptate est esse vel. Est consequatur doloremque quia debitis culpa nihil. Vero sit aut.\n \rIure fugit repudiandae similique eaque cumque sunt quis similique sint. Qui eos laudantium impedit omnis occaecati. Consequatur veniam explicabo minus. Fugiat iure ipsum quisquam iure quo voluptate libero.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=26.167708825873515',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 2,
      Category: {
        id: 2,
        name: '日本料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 43,
      name: 'Dr. Vella Streich',
      tel: '(336) 550-2975',
      address: '12808 Kris Field',
      opening_hours: '08:00',
      description:
        'A aut vero tenetur. Magnam officia iure. Vel nihil ab quod saepe accusamus aliquam iure mollitia molestiae. Sed hic sed ratione ut earum est quis. Qui ad eos pariatur.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=52.301211478657805',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 2,
      Category: {
        id: 2,
        name: '日本料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 44,
      name: 'Simone Stark',
      tel: '(399) 472-3179 x0303',
      address: '8322 Demetris Prairie',
      opening_hours: '08:00',
      description:
        'Exercitationem aliquam corporis quam.\nDignissimos est fugiat ut molestiae impedit.\nSint adipisci esse.\nVel quae aut tenetur nihil sapiente totam sit magnam.\nCulpa iusto ex distinctio eos.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=38.536809030289106',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 4,
      Category: {
        id: 4,
        name: '墨西哥料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 45,
      name: 'Matteo Jones',
      tel: '185.611.0366 x3247',
      address: '0319 Strosin Neck',
      opening_hours: '08:00',
      description: 'sit',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=55.70455977294664',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 3,
      Category: {
        id: 3,
        name: '義大利料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 46,
      name: 'Roosevelt Ullrich',
      tel: '(049) 804-7540 x412',
      address: '22289 Kari Cove',
      opening_hours: '08:00',
      description:
        'Animi est accusantium vel vero doloribus quos facere. Molestias vero qui ut. Aut nulla est et molestiae. Optio rem nemo commodi impedit minus. Sed fugit blanditiis quis. Esse nihil omnis eos.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=58.78562376832763',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 3,
      Category: {
        id: 3,
        name: '義大利料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 47,
      name: 'Angus Hagenes',
      tel: '1-943-026-0855',
      address: '2755 Addie Ford',
      opening_hours: '08:00',
      description:
        'Et praesentium impedit ipsa praesentium.\nQuas recusandae explicabo aut quo sunt amet aspernatur.\nProvident fugit soluta reprehenderit occaecati ut et.\nMagnam ut quos sunt aut recusandae sit magni.\nEst qui adipisci.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=57.45207596628526',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 4,
      Category: {
        id: 4,
        name: '墨西哥料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 48,
      name: 'Marjolaine Lang',
      tel: '(046) 941-9555 x1746',
      address: '7230 Lorine Land',
      opening_hours: '08:00',
      description:
        'Dignissimos ex voluptatem velit. Qui aut omnis doloremque est magni dolore sequi quis delectus. Mollitia placeat repudiandae recusandae. Nisi quia doloremque et. Saepe voluptas dolor pariatur occaecati.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=71.52453105757859',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 5,
      Category: {
        id: 5,
        name: '素食料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 49,
      name: 'Bria Jast',
      tel: '795.421.7038',
      address: '55716 Rowena Unions',
      opening_hours: '08:00',
      description:
        'Consectetur dolore ipsa sit mollitia.\nEaque molestias atque sit veniam sunt error laboriosam molestias et.\nDolorem in accusamus ipsa sunt.\nNeque et non sint ex delectus et possimus.\nMaiores ut earum reiciendis et occaecati fugit iste eaque necessitatibus.',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=9.739880048301753',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 5,
      Category: {
        id: 5,
        name: '素食料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    },
    {
      id: 50,
      name: 'Aron Runte',
      tel: '1-599-600-9422 x11673',
      address: '910 Zola Hill',
      opening_hours: '08:00',
      description: 'sapiente',
      image:
        'https://loremflickr.com/320/240/restaurant,food/?random=60.29197392042607',
      viewCounts: 0,
      createdAt: '2021-06-30T10:09:02.000Z',
      updatedAt: '2021-06-30T10:09:02.000Z',
      CategoryId: 3,
      Category: {
        id: 3,
        name: '義大利料理',
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z'
      }
    }
  ]
}

export default {
  data() {
    return {
      restaurants: []
    }
  },
  created() {
    this.fetchRestaurants()
  },
  methods: {
    fetchRestaurants() {
      this.restaurants = dummyData.restaurants
    },
    deleteRestaurant(restaurantId) {
      this.restaurants = this.restaurants.filter(
        restaurant => restaurant.id !== restaurantId
      )
    }
  }
}
</script>
