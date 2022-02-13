<template>
  <v-container>
    <center><h1 class="p1">Product Page</h1></center>
    <v-container class="d-flex flex-wrap">
      <v-card
        class="mx-auto mb-5"
        max-width="400"
        v-for="(i, index) in productlist"
        :key="index"
      >
        <v-img class="green--text align-end" height="200px" :src="i.image">
          <v-card-title class="textColor">{{ i.title }}</v-card-title>
        </v-img>

        <v-card-subtitle class="pb-0">{{ i.category }}</v-card-subtitle>
        <v-card-text class="text--primary">
          <div>{{ "$" + i.price }}</div>
        </v-card-text>

        <v-card-actions>
          <v-btn color="primary" @click="addCart(i)">ADD </v-btn>
          <v-btn
            color="warning"
            :to="{
              name: 'productdetail',
              params: {
                id: i.id,
                description: i.description,
                img: i.image,
                price: i.price,
                rating: i.rating,
              },
            }"
            >Detail</v-btn
          >
        </v-card-actions>
      </v-card>
    </v-container>
    <div class="row">
      <div class="col-md-4">
        <router-view :key="$route.path"></router-view>
      </div>
      <div class="col-md-8" v-if="carts != 0">
        <h4>Cart</h4>
        <table class="table table-striped">
          <thead>
            <tr align="center">
              <th scope="col">Picture</th>
              <th scope="col">Name</th>
              <th scope="col">Price</th>
              <th scope="col">Quantity</th>
              <th scope="col">Total</th>
              <th scope="col">Remove</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(product, index) in carts" :key="index" align="center">
              <td>
                <img :src="product.img" alt="" width="60px" height="60px" />
              </td>
              <td>{{ product.name }}</td>
              <td>{{ product.price }}</td>
              <td>
                <i
                  class="fas fa-minus quantity-minus"
                  @click="minusQTY(product)"
                ></i
                >{{ product.quantity
                }}<i
                  class="fas fa-plus quantity-plus"
                  @click="plusQTY(product)"
                ></i>
              </td>
              <td>{{ product.total }}</td>
              <td>
                <v-btn color="error" @click="removeProduct(product)"
                  ><i class="fa fa-trash"></i
                ></v-btn>
              </td>
            </tr>
          </tbody>
          <tbody align="center">
            <td></td>
            <td></td>
            <td></td>
            <td><h5>Total price</h5></td>
            <td>
              <h6>{{ total() }}</h6>
            </td>
            <td>
              <v-btn class="success" onClick="window.location.reload();"
                >- Pay -</v-btn
              >
            </td>
          </tbody>
        </table>
      </div>
    </div>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      carts: [],
      one: 0,
      two: 0,
      three: 0,
      four: 0,
      five: 0,
      six: 0,
      seven: 0,
      eight: 0,
      nine: 0,
      ten: 0,
      eleven: 0,
      twelve: 0,

      productlist: [
        {
          id: 1,
          title: "Fjallraven - Foldsack No. 1 Backpack, Fits 15 Laptops",
          price: 109.95,
          description:
            "Your perfect pack for everyday use and walks in the forest. Stash your laptop (up to 15 inches) in the padded sleeve, your everyday",
          category: "men's clothing",
          image: "https://fakestoreapi.com/img/81fPKd-2AYL._AC_SL1500_.jpg",

          rating: {
            rate: 3.9,
            count: 120,
          },
          active: false,
        },

        {
          id: 2,
          title: "Mens Casual Premium Slim Fit T-Shirts ",
          price: 22.3,
          description:
            "Slim-fitting style, contrast raglan long sleeve, three-button henley placket, light weight & soft fabric for breathable and comfortable wearing. And Solid stitched shirts with round neck made for durability and a great fit for casual fashion wear and diehard baseball fans. The Henley style round neckline includes a three-button placket.",
          category: "men's clothing",
          image:
            "https://fakestoreapi.com/img/71-3HjGNDUL._AC_SY879._SX._UX._SY._UY_.jpg",

          rating: {
            rate: 4.1,
            count: 259,
          },
          active: false,
        },

        {
          id: 3,
          title: "Mens Cotton Jacket",
          price: 55.99,
          description:
            "great outerwear jackets for Spring/Autumn/Winter, suitable for many occasions, such as working, hiking, camping, mountain/rock climbing, cycling, traveling or other outdoors. Good gift choice for you or your family member. A warm hearted love to Father, husband or son in this thanksgiving or Christmas Day.",
          category: "men's clothing",
          image: "https://fakestoreapi.com/img/71li-ujtlUL._AC_UX679_.jpg",

          rating: {
            rate: 4.7,
            count: 500,
          },
          active: false,
        },

        {
          id: 4,
          title: "Mens Casual Slim Fit",
          price: 15.99,
          description:
            "The color could be slightly different between on the screen and in practice. / Please note that body builds vary by person, therefore, detailed size information should be reviewed below on the product description.",
          category: "men's clothing",
          image: "https://fakestoreapi.com/img/71YXzeOuslL._AC_UY879_.jpg",

          rating: {
            rate: 2.1,
            count: 430,
          },
          active: false,
        },

        {
          id: 5,
          title:
            "John Hardy Women's Legends Naga Gold & Silver Dragon Station Chain Bracelet",
          price: 695,
          description:
            "From our Legends Collection, the Naga was inspired by the mythical water dragon that protects the ocean's pearl. Wear facing inward to be bestowed with love and abundance, or outward for protection.",
          category: "jewelery",
          image:
            "https://fakestoreapi.com/img/71pWzhdJNwL._AC_UL640_QL65_ML3_.jpg",

          rating: {
            rate: 4.6,
            count: 400,
          },
          active: false,
        },

        {
          id: 6,
          title: "Solid Gold Petite Micropave ",
          price: 168,
          description:
            "Satisfaction Guaranteed. Return or exchange any order within 30 days.Designed and sold by Hafeez Center in the United States. Satisfaction Guaranteed. Return or exchange any order within 30 days.",
          category: "jewelery",
          image:
            "https://fakestoreapi.com/img/61sbMiUnoGL._AC_UL640_QL65_ML3_.jpg",

          rating: {
            rate: 3.9,
            count: 70,
          },
          active: false,
        },

        {
          id: 7,
          title: "White Gold Plated Princess",
          price: 9.99,
          description:
            "Classic Created Wedding Engagement Solitaire Diamond Promise Ring for Her. Gifts to spoil your love more for Engagement, Wedding, Anniversary, Valentine's Day...",
          category: "jewelery",
          image:
            "https://fakestoreapi.com/img/71YAIFU48IL._AC_UL640_QL65_ML3_.jpg",

          rating: {
            rate: 3,
            count: 400,
          },
          active: false,
        },

        {
          id: 8,
          title: "Pierced Owl Rose Gold Plated Stainless Steel Double",
          price: 10.99,
          description:
            "Rose Gold Plated Double Flared Tunnel Plug Earrings. Made of 316L Stainless Steel",
          category: "jewelery",
          image:
            "https://fakestoreapi.com/img/51UDEzMJVpL._AC_UL640_QL65_ML3_.jpg",

          rating: {
            rate: 1.9,
            count: 100,
          },
          active: false,
        },

        {
          id: 9,
          title: "WD 2TB Elements Portable External Hard Drive - USB 3.0 ",
          price: 64,
          description:
            "USB 3.0 and USB 2.0 Compatibility Fast data transfers Improve PC Performance High Capacity; Compatibility Formatted NTFS for Windows 10, Windows 8.1, Windows 7; Reformatting may be required for other operating systems; Compatibility may vary depending on user’s hardware configuration and operating system",
          category: "electronics",
          image: "https://fakestoreapi.com/img/61IBBVJvSDL._AC_SY879_.jpg",

          rating: {
            rate: 3.3,
            count: 203,
          },
          active: false,
        },

        {
          id: 10,
          title: "SanDisk SSD PLUS 1TB Internal SSD - SATA III 6 Gb/s",
          price: 109,
          description:
            "Easy upgrade for faster boot up, shutdown, application load and response (As compared to 5400 RPM SATA 2.5” hard drive; Based on published specifications and internal benchmarking tests using PCMark vantage scores) Boosts burst write performance, making it ideal for typical PC workloads The perfect balance of performance and reliability Read/write speeds of up to 535MB/s/450MB/s (Based on internal testing; Performance may vary depending upon drive capacity, host device, OS and application.)",
          category: "electronics",
          image: "https://fakestoreapi.com/img/61U7T1koQqL._AC_SX679_.jpg",

          rating: {
            rate: 2.9,
            count: 470,
          },
          active: false,
        },

        {
          id: 11,
          title:
            "Silicon Power 256GB SSD 3D NAND A55 SLC Cache Performance Boost SATA III 2.5",
          price: 109,
          description:
            "3D NAND flash are applied to deliver high transfer speeds Remarkable transfer speeds that enable faster bootup and improved overall system performance. The advanced SLC Cache Technology allows performance boost and longer lifespan 7mm slim design suitable for Ultrabooks and Ultra-slim notebooks. Supports TRIM command, Garbage Collection technology, RAID, and ECC (Error Checking & Correction) to provide the optimized performance and enhanced reliability.",
          category: "electronics",
          image: "https://fakestoreapi.com/img/71kWymZ+c+L._AC_SX679_.jpg",

          rating: {
            rate: 4.8,
            count: 319,
          },
          active: false,
        },

        {
          id: 12,
          title:
            "WD 4TB Gaming Drive Works with Playstation 4 Portable External Hard Drive",
          price: 114,
          description:
            "Expand your PS4 gaming experience, Play anywhere Fast and easy, setup Sleek design with high capacity, 3-year manufacturer's limited warranty",
          category: "electronics",
          image: "https://fakestoreapi.com/img/61mtL65D4cL._AC_SX679_.jpg",

          rating: {
            rate: 4.8,
            count: 400,
          },
          active: false,
        },
      ],
    };
  },
  methods: {
    addCart: function (i) {
      if (i.id == 1) {
        this.one += 1;
        if (this.one <= 1) {
          this.pushData(i);
        } else {
          var Oone = this.findID(i);
          this.carts[Oone].quantity += 1;
          this.carts[Oone].total =
            this.carts[Oone].quantity * this.carts[Oone].price;
        }
      }
      if (i.id == 2) {
        this.two += 1;
        if (this.two <= 1) {
          this.pushData(i);
        } else {
          var Ttwo = this.findID(i);
          this.carts[Ttwo].quantity += 1;
          this.carts[Ttwo].total =
            this.carts[Ttwo].quantity * this.carts[Ttwo].price;
        }
      }
      if (i.id == 3) {
        this.three += 1;
        if (this.three <= 1) {
          this.pushData(i);
        } else {
          var Tthree = this.findID(i);
          this.carts[Tthree].quantity += 1;
          this.carts[Tthree].total =
            this.carts[Tthree].quantity * this.carts[Tthree].price;
        }
      }
      if (i.id == 4) {
        this.four += 1;
        if (this.four <= 1) {
          this.pushData(i);
        } else {
          var Ffour = this.findID(i);
          this.carts[Ffour].quantity += 1;
          this.carts[Ffour].total =
            this.carts[Ffour].quantity * this.carts[Ffour].price;
        }
      }
      if (i.id == 5) {
        this.five += 1;
        if (this.five <= 1) {
          this.pushData(i);
        } else {
          var Ffive = this.findID(i);
          this.carts[Ffive].quantity += 1;
          this.carts[Ffive].total =
            this.carts[Ffive].quantity * this.carts[Ffive].price;
        }
      }
      if (i.id == 6) {
        this.six += 1;
        if (this.six <= 1) {
          this.pushData(i);
        } else {
          var Ssix = this.findID(i);
          this.carts[Ssix].quantity += 1;
          this.carts[Ssix].total =
            this.carts[Ssix].quantity * this.carts[Ssix].price;
        }
      }
      if (i.id == 7) {
        this.seven += 1;
        if (this.seven <= 1) {
          this.pushData(i);
        } else {
          var Sseven = this.findID(i);
          this.carts[Sseven].quantity += 1;
          this.carts[Sseven].total =
            this.carts[Sseven].quantity * this.carts[Sseven].price;
        }
      }
      if (i.id == 8) {
        this.eight += 1;
        if (this.eight <= 1) {
          this.pushData(i);
        } else {
          var Eeight = this.findID(i);
          this.carts[Eeight].quantity += 1;
          this.carts[Eeight].total =
            this.carts[Eeight].quantity * this.carts[Eeight].price;
        }
      }
      if (i.id == 9) {
        this.nine += 1;
        if (this.nine <= 1) {
          this.pushData(i);
        } else {
          var Nnine = this.findID(i);
          this.carts[Nnine].quantity += 1;
          this.carts[Nnine].total =
            this.carts[Nnine].quantity * this.carts[Nnine].price;
        }
      }
      if (i.id == 10) {
        this.ten += 1;
        if (this.ten <= 1) {
          this.pushData(i);
        } else {
          var Tten = this.findID(i);
          this.carts[Tten].quantity += 1;
          this.carts[Tten].total =
            this.carts[Tten].quantity * this.carts[Tten].price;
        }
      }

      if (i.id == 11) {
        this.eleven += 1;
        if (this.eleven <= 1) {
          this.pushData(i);
        } else {
          var Eeleven = this.findID(i);
          this.carts[Eeleven].quantity += 1;
          this.carts[Eeleven].total =
            this.carts[Eeleven].quantity * this.carts[Eeleven].price;
        }
      }
      if (i.id == 12) {
        this.twelve += 1;
        if (this.twelve <= 1) {
          this.pushData(i);
        } else {
          var Ttwelve = this.findID(i);
          this.carts[Ttwelve].quantity += 1;
          this.carts[Ttwelve].total =
            this.carts[Ttwelve].quantity * this.carts[Ttwelve].price;
        }
      }
    },
    pushData(i) {
      this.carts.push({
        id: i.id,
        name: i.title,
        price: i.price,
        img: i.image,
        quantity: 1,
        total: i.price,
      });
    },
    findID: function (i) {
      for (var x = 0; x < this.carts.length; x++) {
        if (this.carts[x].id == i.id) {
          return x;
        }
      }
      return -1;
    },
    minusQTY: function (product) {
      product.quantity -= 1;
      if (product.quantity <= 1) {
        product.quantity = 1;
      }
      product.total = product.price * product.quantity;
    },
    plusQTY: function (product) {
      product.quantity += 1;
      product.total = product.price * product.quantity;
    },
    removeProduct: function (product) {
      if (confirm("Do you want to remove? ")) {
        var index = this.carts.indexOf(product);
        this.carts.splice(index, 1);
        if (product.id == 1) {
          this.one = 0;
        }
        if (product.id == 2) {
          this.two = 0;
        }
        if (product.id == 3) {
          this.three = 0;
        }
        if (product.id == 4) {
          this.four = 0;
        }
        if (product.id == 5) {
          this.five = 0;
        }
        if (product.id == 6) {
          this.six = 0;
        }
        if (product.id == 7) {
          this.seven = 0;
        }
        if (product.id == 8) {
          this.eight = 0;
        }
        if (product.id == 9) {
          this.nine = 0;
        }
        if (product.id == 10) {
          this.ten = 0;
        }
        if (product.id == 11) {
          this.eleven = 0;
        }
        if (product.id == 12) {
          this.twelve = 0;
        }
      }
    },
    total: function () {
      var sum = 0;
      this.carts.forEach(function (i) {
        sum += i.total;
      });
      return sum;
    },
  },
};
</script>

<style scoped>
.quantity-minus {
  cursor: pointer;
  margin-right: 20px;
}
.quantity-plus {
  cursor: pointer;
  margin-left: 20px;
}

@keyframes gradient {
  0% {
    background-position: 0% 50%;
  }
  100% {
    background-position: 100% 0%;
  }
}

.textColor {
  background: linear-gradient(80deg, #979494, rgb(233, 220, 35));
  background-size: 50%;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: gradient 4s infinite;
}
</style>
