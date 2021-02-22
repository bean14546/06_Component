<template>
  <div class="hello">
    <div class="container">
      <h2 class="nameStore">ร้านขายขนมหวาน</h2>
      <hr />
      <div class="row">
        <div class="col-md-3 col-sm-4" v-for="item in products" :key="item">
          <b-card :title="item.name" :img-src="item.image" style="max-width: 20rem" class="mb-2">
            <b-card-text>ราคา&nbsp;{{ item.price }}&nbsp;บาท</b-card-text>

            <b-button href="#" variant="dark" @click="addCart(item)">Add to cart</b-button>
          </b-card>
        </div>
      </div>

      <table align="center" class="table col-md-12" v-if="cart!=0">
        <thead class="table-dark">
          <tr>
            <th scope="col">ภาพ</th>
            <th scope="col">ชื่อ</th>
            <th scope="col">ราคา</th>
            <th scope="col">จำนวณ</th>
            <th scope="col">รวม</th>
            <th scope="col">ลบ</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="product in cart" :key="product">
            <td>
              <img :src="product.image" width="80px" height="60px" />
            </td>
            <td>{{product.name}}</td>
            <td>{{product.price}}</td>
            <td>
              <i class="fa fa-minus qty-minus" @click="minusQty(product)"></i>
              {{product.qty}}
              <i class="fa fa-plus qty-plus" @click="plusQty(product)"></i>
            </td>
            <td>{{product.total}}</td>
            <td>
              <button @click="removeProduct(product)">ลบ</button>
            </td>
          </tr>
        </tbody>
      </table>

      <h4 class="price" v-if="cart!=0">ยอดชำระเงินทั้งหมด&nbsp;{{total()}}&nbsp;บาท</h4>
      <hr />
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  // props: {
  //   msg: String,
  // },

  data() {
    return {
      cart: [],
      p1: 0,
      p2: 0,
      p3: 0,
      p4: 0,
      p5: 0,
      p6: 0,
      p7: 0,
      p8: 0,
      products: [
        {
          id: 1,
          name: "มะยงชิดข้าวเหนียวมูน",
          price: 40,
          image:
            "https://img.wongnai.com/p/1920x0/2018/04/12/c5dea6a72da043839b71f33c4506a6a1.jpg",
          state: false,
        },
        {
          id: 2,
          name: "ซาหริ่มอันชัน",
          price: 30,
          image:
            "https://img.wongnai.com/p/1920x0/2018/07/26/c134853612734d61894c7810b66f2a6b.jpg",
          state: false,
        },
        {
          id: 3,
          name: "มะม่วงหาวลอยแก้ว",
          price: 20,
          image:
            "https://img.wongnai.com/p/1920x0/2018/08/10/9968149533184b958cef50207c7d6b1c.jpg",
          state: false,
        },
        {
          id: 4,
          name: "โดนัทมะม่วง",
          price: 45,
          image:
            "https://img.kapook.com/u/2018/surauch/cooking/co1/summer2.jpg",
          state: false,
        },
        {
          id: 5,
          name: "ลอดช่องสิงคโปร์",
          price: 30,
          image:
            "https://s3-ap-southeast-1.amazonaws.com/photo.wongnai.com/photos/2017/04/11/24cb91e7fa2744db870eb714f0abd915.jpg",
          state: false,
        },
        {
          id: 6,
          name: "ม้าฮ่อ",
          price: 20,
          image:
            "https://img.wongnai.com/p/1920x0/2018/03/01/bd4949f77d284f09879ac19d35d8f80a.jpg",
          state: false,
        },
        {
          id: 7,
          name: "ลูกตาลลอยแก้ว",
          price: 25,
          image:
            "https://img.wongnai.com/p/l/2017/06/26/0b0c797e61e84be5ad4775fe31f01b8c.jpg",
          state: false,
        },
        {
          id: 8,
          name: "เครปใบเตย",
          price: 40,
          image:
            "https://img.kapook.com/u/2018/surauch/cooking/co1/summer11.jpg",
          state: false,
        },
      ],
    };
  },
  methods: {
    addCart: function (item) {
      var found;
      if (item.id == 1) {
        this.p1 += 1;
        if (this.p1 <= 1) {
          //ซื้อรอบเดียว
          this.pushData(item);
        } else {
          //ซื้อซ้ำ
          found = this.findID(item);
          this.cart[found].qty += 1;
          this.cart[found].total =
            this.cart[found].qty * this.cart[found].price;
        }
      } else if (item.id == 2) {
        //ซื้ออย่างอื่น
        this.p2 += 1;
        if (this.p2 <= 1) {
          //ซื้อรอบเดียว
          this.pushData(item);
        } else {
          //ซื้อซ้ำ
          found = this.findID(item);
          this.cart[found].qty += 1;
          this.cart[found].total =
            this.cart[found].qty * this.cart[found].price;
        }
      } else if (item.id == 3) {
        //ซื้ออย่างอื่น
        this.p3 += 1;
        if (this.p3 <= 1) {
          //ซื้อรอบเดียว
          this.pushData(item);
        } else {
          //ซื้อซ้ำ
          found = this.findID(item);
          this.cart[found].qty += 1;
          this.cart[found].total =
            this.cart[found].qty * this.cart[found].price;
        }
      } else if (item.id == 4) {
        //ซื้ออย่างอื่น
        this.p4 += 1;
        if (this.p3 <= 1) {
          //ซื้อรอบเดียว
          this.pushData(item);
        } else {
          //ซื้อซ้ำ
          found = this.findID(item);
          this.cart[found].qty += 1;
          this.cart[found].total =
            this.cart[found].qty * this.cart[found].price;
        }
      } else if (item.id == 5) {
        //ซื้ออย่างอื่น
        this.p5 += 1;
        if (this.p5 <= 1) {
          //ซื้อรอบเดียว
          this.pushData(item);
        } else {
          //ซื้อซ้ำ
          found = this.findID(item);
          this.cart[found].qty += 1;
          this.cart[found].total =
            this.cart[found].qty * this.cart[found].price;
        }
      } else if (item.id == 6) {
        //ซื้ออย่างอื่น
        this.p6 += 1;
        if (this.p6 <= 1) {
          //ซื้อรอบเดียว
          this.pushData(item);
        } else {
          //ซื้อซ้ำ
          found = this.findID(item);
          this.cart[found].qty += 1;
          this.cart[found].total =
            this.cart[found].qty * this.cart[found].price;
        }
      } else if (item.id == 7) {
        //ซื้ออย่างอื่น
        this.p7 += 1;
        if (this.p7 <= 1) {
          //ซื้อรอบเดียว
          this.pushData(item);
        } else {
          //ซื้อซ้ำ
          found = this.findID(item);
          this.cart[found].qty += 1;
          this.cart[found].total =
            this.cart[found].qty * this.cart[found].price;
        }
      } else if (item.id == 8) {
        //ซื้ออย่างอื่น
        this.p8 += 1;
        if (this.p8 <= 1) {
          //ซื้อรอบเดียว
          this.pushData(item);
        } else {
          //ซื้อซ้ำ
          found = this.findID(item);
          this.cart[found].qty += 1;
          this.cart[found].total =
            this.cart[found].qty * this.cart[found].price;
        }
      }
    },
    pushData(item) {
      this.cart.push({
        id: item.id,
        name: item.name,
        price: item.price,
        image: item.image,
        qty: 1,
        total: item.price,
      });
    },
    findID: function (item) {
      for (var i = 0; i < this.cart.length; i++) {
        if (this.cart[i].id == item.id) {
          return i; //ตำแหนงสินค้าที่ค้นเจอในตะกร้า
        }
      }
      return -1;
    },
    minusQty: function (product) {
      product.qty -= 1;
      if (product.qty <= 1) {
        product.qty = 1;
      }
      product.total = product.qty * product.price;
    },
    plusQty: function (product) {
      product.qty += 1;
      product.total = product.qty * product.price;
    },
    removeProduct(product) {
      if (confirm("คุณต้องการลบหรือไม่ ?")) {
        var index = this.cart.indexOf(product);
        this.cart.splice(index, 1);
        if (product.id == 1) {
          this.p1 = 0;
        } else {
          this.p2 = 0;
        }
      }
    },
    total: function () {
      var sum = 0;
      this.cart.forEach(function (item) {
        sum += item.total;
      });
      return sum;
    },
  },
};
</script>

// <!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.nameStore {
  margin-bottom: 10px;
}
.qty-minus {
  cursor: pointer;
  margin-right: 10px;
}
.qty-plus {
  cursor: pointer;
  margin-left: 10px;
}
.table {
  margin-top: 20px;
}
.price {
  margin-bottom: 20px;
}
</style>
