<template>
  <div class="container py-5">
    <form @submit.stop.prevent="handleSubmit">
      <div class="form-group">
        <label for="name">Name</label>
        <input
          id="name"
          type="text"
          name="name"
          class="form-control"
          placeholder="Enter Name"
          required
        />
      </div>

      <div class="form-group">
        <label for="image">Image</label>

        <img
          v-if="user.image"
          :src="user.image"
          class="d-block img-thumbnail mb-3"
          width="200"
          height="200"
        />
        <input
          id="image"
          type="file"
          name="image"
          accept="image/*"
          class="form-control-file"
          @change="handleFileChange"
        />
      </div>

      <button type="submit" class="btn btn-primary">
        Submit
      </button>
    </form>
  </div>
</template>

<script>
const dummyData = {
  profile: {
    id: 1,
    name: 'root',
    email: 'root@example.com',
    password: '$2a$10$6TWwUj1MV2p7dBBHgzyRsu2PWHy5QaNcMhGcKy9UWsjT7tyaDZynC',
    isAdmin: true,
    image: null,
    createdAt: '2021-06-30T10:09:01.000Z',
    updatedAt: '2021-06-30T10:09:01.000Z',
    Comments: [
      {
        id: 3,
        text:
          'Tenetur totam vel itaque repudiandae aut quia fugit culpa omnis.',
        UserId: 1,
        RestaurantId: 3,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 2
        }
      },
      {
        id: 12,
        text:
          'Eum voluptas ipsa aspernatur qui molestiae voluptatem sed sed voluptas.',
        UserId: 1,
        RestaurantId: 12,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 3
        }
      },
      {
        id: 13,
        text: 'Aspernatur voluptatem incidunt repellat numquam et.',
        UserId: 1,
        RestaurantId: 13,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 3
        }
      },
      {
        id: 19,
        text: 'Aperiam veritatis itaque vel fugit sed.',
        UserId: 1,
        RestaurantId: 19,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 4
        }
      },
      {
        id: 22,
        text: 'Officia magnam non consequatur et.',
        UserId: 1,
        RestaurantId: 22,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 3
        }
      },
      {
        id: 23,
        text: 'Totam eaque eligendi deserunt.',
        UserId: 1,
        RestaurantId: 23,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 4
        }
      },
      {
        id: 24,
        text: 'Ipsam totam ut omnis laboriosam.',
        UserId: 1,
        RestaurantId: 24,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 3
        }
      },
      {
        id: 27,
        text: 'Est accusamus enim fugiat officia aperiam.',
        UserId: 1,
        RestaurantId: 27,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 5
        }
      },
      {
        id: 28,
        text: 'Quia quaerat et.',
        UserId: 1,
        RestaurantId: 28,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 2
        }
      },
      {
        id: 30,
        text: 'Aliquam molestiae illum sapiente quisquam.',
        UserId: 1,
        RestaurantId: 30,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 4
        }
      },
      {
        id: 31,
        text:
          'Aspernatur necessitatibus in excepturi omnis quasi a accusantium itaque natus.',
        UserId: 1,
        RestaurantId: 31,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 3
        }
      },
      {
        id: 34,
        text: 'Repudiandae magni iste aliquam quisquam.',
        UserId: 1,
        RestaurantId: 34,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 1
        }
      },
      {
        id: 42,
        text:
          'Eum voluptatem necessitatibus voluptas vel praesentium rerum dolor doloribus ipsa.',
        UserId: 1,
        RestaurantId: 42,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 2
        }
      },
      {
        id: 45,
        text: 'Iste nesciunt odit in voluptatum corporis veniam dicta.',
        UserId: 1,
        RestaurantId: 45,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 3
        }
      },
      {
        id: 50,
        text: 'Quam dolores harum.',
        UserId: 1,
        RestaurantId: 50,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 3
        }
      },
      {
        id: 61,
        text: 'Dolor et qui minima rerum consequatur quia voluptates.',
        UserId: 1,
        RestaurantId: 11,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 2
        }
      },
      {
        id: 64,
        text: 'Quidem sequi natus in.',
        UserId: 1,
        RestaurantId: 14,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 4
        }
      },
      {
        id: 65,
        text:
          'Quidem sint repudiandae sit exercitationem beatae natus commodi vitae delectus.',
        UserId: 1,
        RestaurantId: 15,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 2
        }
      },
      {
        id: 72,
        text: 'Voluptatem sint non.',
        UserId: 1,
        RestaurantId: 22,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 3
        }
      },
      {
        id: 74,
        text: 'Dicta aut sapiente sint autem quaerat adipisci soluta.',
        UserId: 1,
        RestaurantId: 24,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 3
        }
      },
      {
        id: 75,
        text: 'Repellat eum tenetur reiciendis.',
        UserId: 1,
        RestaurantId: 25,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 5
        }
      },
      {
        id: 77,
        text: 'Expedita qui rerum perspiciatis facilis cumque quia qui.',
        UserId: 1,
        RestaurantId: 27,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 5
        }
      },
      {
        id: 83,
        text: 'Fugiat placeat vero.',
        UserId: 1,
        RestaurantId: 33,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 4
        }
      },
      {
        id: 87,
        text: 'Quae perspiciatis nisi amet nam sit non labore eaque.',
        UserId: 1,
        RestaurantId: 37,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 1
        }
      },
      {
        id: 94,
        text: 'Perspiciatis quos ea amet.',
        UserId: 1,
        RestaurantId: 44,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 4
        }
      },
      {
        id: 95,
        text: 'Explicabo nesciunt accusantium iure maiores.',
        UserId: 1,
        RestaurantId: 45,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 3
        }
      },
      {
        id: 99,
        text: 'Qui aut sequi expedita vitae.',
        UserId: 1,
        RestaurantId: 49,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 5
        }
      },
      {
        id: 100,
        text: 'Id dolor et dolorem dicta eius.',
        UserId: 1,
        RestaurantId: 50,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 3
        }
      },
      {
        id: 101,
        text:
          'Officiis neque exercitationem est nihil distinctio sit deleniti et vitae.',
        UserId: 1,
        RestaurantId: 1,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 5
        }
      },
      {
        id: 112,
        text: 'Dolorem officia eum nemo ad quod sunt quia necessitatibus.',
        UserId: 1,
        RestaurantId: 12,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 3
        }
      },
      {
        id: 113,
        text: 'Quia ratione et.',
        UserId: 1,
        RestaurantId: 13,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 3
        }
      },
      {
        id: 115,
        text: 'Sed ea unde nihil et cum.',
        UserId: 1,
        RestaurantId: 15,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 2
        }
      },
      {
        id: 123,
        text: 'Fugit reprehenderit dolor.',
        UserId: 1,
        RestaurantId: 23,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 4
        }
      },
      {
        id: 129,
        text:
          'Expedita nam expedita dolor voluptatum consequatur officiis quam quis.',
        UserId: 1,
        RestaurantId: 29,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 3
        }
      },
      {
        id: 136,
        text: 'Modi modi aperiam iste eligendi sed.',
        UserId: 1,
        RestaurantId: 36,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 3
        }
      },
      {
        id: 142,
        text: 'Ut officiis ut quis cum assumenda.',
        UserId: 1,
        RestaurantId: 42,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 2
        }
      },
      {
        id: 146,
        text: 'Aut expedita laborum omnis eligendi.',
        UserId: 1,
        RestaurantId: 46,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 3
        }
      },
      {
        id: 147,
        text: 'Vel molestiae accusamus.',
        UserId: 1,
        RestaurantId: 47,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 4
        }
      },
      {
        id: 149,
        text: 'Commodi quo qui qui non adipisci magni.',
        UserId: 1,
        RestaurantId: 49,
        createdAt: '2021-06-30T10:09:02.000Z',
        updatedAt: '2021-06-30T10:09:02.000Z',
        Restaurant: {
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
          CategoryId: 5
        }
      }
    ],
    FavoritedRestaurants: [],
    Followers: [],
    Followings: []
  },
  isFollowed: false
}

export default {
  data() {
    return {
      user: {
        id: -1,
        name: '',
        image: ''
      }
    }
  },
  methods: {
    handleAfterSubmit(formData) {
      // 透過 API 將表單資料送到伺服器
      for (const [name, value] of formData.entries()) {
        console.log(name + ': ' + value)
      }
    },
    fetchUser(userID) {
      console.log('fetchUser id:', userID)
      const { profile } = dummyData
      this.user = {
        ...this.user,
        id: profile.id,
        name: profile.name,
        image: profile.image
      }
    },
    handleFileChange(e) {
      const { files } = e.target

      if (files.length === 0) {
        // 使用者沒有選擇上傳的檔案
        this.user.image = ''
      } else {
        // 否則產生預覽圖
        const imageURL = window.URL.createObjectURL(files[0])
        this.user.image = imageURL
      }
    },
    handleSubmit(e) {
      const form = e.target
      const formData = new FormData(form)
      console.log(e.target, formData)
      // this.$emit('after-submit', formData)
      this.$router.push(`/users/${this.user.id}`)
    }
  },
  created() {
    const { id } = this.$route.params
    this.fetchUser(id)
  }
}
</script>
