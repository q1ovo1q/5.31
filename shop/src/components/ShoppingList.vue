<template>
  <div>
    <h1>热销爆款</h1>
    <!-- 商品列表 -->
    <div class="shop-list">
      <!-- 导航 -->
      <div class="list-nav">
        <ul>
          <li @click="selectTab('空调')" :class="{ active: selectedTab === '空调' }">空调</li>
          <li @click="selectTab('电视')" :class="{ active: selectedTab === '电视' }">电视</li>
          <li @click="selectTab('冰箱')" :class="{ active: selectedTab === '冰箱' }">冰箱</li>
          <li @click="selectTab('洗衣机')" :class="{ active: selectedTab === '洗衣机' }">洗衣机</li>
          <li @click="selectTab('热水器')" :class="{ active: selectedTab === '热水器' }">热水器</li>
          <li @click="selectTab('生活电器')" :class="{ active: selectedTab === '生活电器' }">生活电器</li>
        </ul>
      </div>
      <!-- 商品列表 -->
      <div class="tab-content">
        <div v-if="selectedTab === '空调'">
          <ul>
            <li v-for="item in airConditioner" :key="item.id">
              <img :src="item.imgSrc" alt="">
              <p>{{ item.name }}</p>
              <p>￥{{ item.dan }}元</p>
              <button @click="addg(item)">添加到购物车</button>
            </li>
          </ul>
        </div>
        <div v-if="selectedTab === '电视'">
          <ul>
            <li v-for="item in tv" :key="item.id">
              <img :src="item.imgSrc" alt="">
              <p>{{ item.name }}</p>
              <p>￥{{ item.dan }}元</p>
              <button @click="addg(item)">添加到购物车</button>
            </li>
          </ul>
        </div>
        <div v-if="selectedTab === '冰箱'">
          <ul>
            <li v-for="item in fridge" :key="item.id">
              <img :src="item.imgSrc" alt="">
              <p>{{ item.name }}</p>
              <p>￥{{ item.dan }}元</p>
              <button @click="addg(item)">添加到购物车</button>
            </li>
          </ul>
        </div>
        <div v-if="selectedTab === '洗衣机'">
          <ul>
            <li v-for="item in washingMachine" :key="item.id">
              <img :src="item.imgSrc" alt="">
              <p>{{ item.name }}</p>
              <p>￥{{ item.dan }}元</p>
              <button @click="addg(item)">添加到购物车</button>
            </li>
          </ul>
        </div>
        <div v-if="selectedTab === '热水器'">
          <ul>
            <li v-for="item in waterHeater" :key="item.id">
              <img :src="item.imgSrc" alt="">
              <p>{{ item.name }}</p>
              <p>￥{{ item.dan }}元</p>
              <button @click="addg(item)">添加到购物车</button>
            </li>
          </ul>
        </div>
        <div v-if="selectedTab === '生活电器'">
          <ul>
            <li v-for="item in homeAppliance" :key="item.id">
              <img :src="item.imgSrc" alt="">
              <p>{{ item.name }}</p>
              <p>￥{{ item.dan }}元</p>
              <button @click="addg(item)">添加到购物车</button>
            </li>
          </ul>
        </div>
      </div>
    </div>
    <!-- 购物车 -->
    <div class="shopping-cart">
      <table>
        <thead>
          <tr>
            <th>全选:<input type="checkbox" v-model="isCheckedAll" /></th>
            <th>序列号</th>
            <th>商品</th>
            <th>图片</th>
            <th>数量</th>
            <th>单价(元)</th>
            <th>金额(元)</th>
            <th>操作</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in shopping" :key="item.id">
            <td><input type="checkbox" v-model="item.checked" /></td>
            <td>{{ index + 1 }}</td>
            <td>{{ item.name }}</td>
            <td><img :src="item.imgSrc" width="80" height="80" /></td>
            <td>
              <button @click="update(item, -1)">-</button>
              <span>{{ item.total }}</span>
              <button @click="update(item, 1)">+</button>
            </td>
            <td>{{ item.dan }}元</td>
            <td>{{ (item.total * item.dan).toFixed(2) }}</td>
            <td><button @click="del(index)">删除</button></td>
          </tr>
        </tbody>
        <tfoot>
          <tr>
            <td colspan="6">总价：<span>{{ getSum }}元</span></td>
            <td>计件：{{ jSum }}</td>
            <td><button>结算</button></td>
          </tr>
        </tfoot>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      shopping: [],
      selectedTab: '空调',
      //空调
      airConditioner: [
        {
          id: 1,
          name: '美的空调一级能效大1.5匹变频冷暖空调',
          imgSrc: 'https://img.alicdn.com/imgextra/i1/6255167485/O1CN01JWQfWj25ABVptrWzp_!!2-saturn_solar.png_360x360xzq75.jpg_.webp',
          dan: 3449.00,
          num: 10
        },
        {
          id: 2,
          name: '美的空调扇冷风机家用制冷小型水空调',
          imgSrc: 'https://img.alicdn.com/imgextra/i3/2973966816/O1CN01McgfqK20DmVi2iKcq_!!2973966816-0-alimamacc.jpg_360x360xzq75.jpg_.webp',
          dan: 999.00,
          num: 10
        },
        {
          id: 3,
          name: '强劲海尔空调大1匹家用新一级变流空调',
          imgSrc: 'https://img.alicdn.com/imgextra/i1/18307420/O1CN01oX0HwC24gPllbyV6c_!!0-saturn_solar.jpg_360x360xzq75.jpg_.webp',
          dan: 3599.00,
          num: 10
        },
        {
          id: 4,
          name: '松下空调新一级能效大1匹家用变频冷暖挂机',
          imgSrc: 'https://img.alicdn.com/imgextra/i4/1666865507/O1CN01wHvkLZ1qYG45cgRPf_!!1666865507-0-alimamacc.jpg_360x360xzq75.jpg_.webp',
          dan: 4999.00,
          num: 10
        },
        {
          id: 5,
          name: '松下空调新一级能效大1匹家用变频冷暖挂机',
          imgSrc: 'https://img.alicdn.com/imgextra/i4/1666865507/O1CN01wHvkLZ1qYG45cgRPf_!!1666865507-0-alimamacc.jpg_360x360xzq75.jpg_.webp',
          dan: 4999.00,
          num: 10
        },
        {
          id: 6,
          name: '松下空调新一级能效大1匹家用变频冷暖挂机',
          imgSrc: 'https://img.alicdn.com/imgextra/i4/1666865507/O1CN01wHvkLZ1qYG45cgRPf_!!1666865507-0-alimamacc.jpg_360x360xzq75.jpg_.webp',
          dan: 4999.00,
          num: 10
        },
      ]
      ,
      //电视
      tv: [
        {
          id: 7,
          name: '海尔电视s60系列',
          imgSrc: 'https://img1.360buyimg.com/n6/jfs/t1/163759/38/45291/140165/6656ee1fF8de9ff64/2d99d7db1de490d0.jpg',
          dan: 3799.00,
          num: 10
        },
        {
          id: 8,
          name: '海尔电视s60系列111',
          imgSrc: 'https://img1.360buyimg.com/n6/jfs/t1/163759/38/45291/140165/6656ee1fF8de9ff64/2d99d7db1de490d0.jpg',
          dan: 3799.00,
          num: 10
        },
      ],
      //冰箱
      fridge: [{
        id: 9,
        name: '西门子502l官方对开门电冰箱',
        imgSrc: 'https://img.alicdn.com/imgextra/i4/32439009/O1CN01Ma5lpj2GQB7MN4LLZ_!!0-saturn_solar.jpg_360x360xzq75.jpg_.webp',
        dan: 7099.00,
        num: 10
      }, {
        id: 10,
        name: '某品牌冰箱22',
        imgSrc: 'https://img.alicdn.com/imgextra/i4/5544534432/O1CN01jzIjQL1ibuK8sHPKs_!!0-saturn_solar.jpg_360x360xzq75.jpg_.webp',
        dan: 3999.00,
        num: 10
      },
      ],
      //洗衣机
      washingMachine: [
        {
          id: 11,
          name: '简真净澈洗衣机',
          imgSrc: 'https://img.alicdn.com/imgextra/i4/2206402570401/O1CN01C6Xjfo1EphgcCOIx9_!!2206402570401-0-alimamacc.jpg_360x360xzq75.jpg_.webp',
          dan: 8499.00,
          num: 10
        },
        {
          id: 12,
          name: '西门子10公斤滚轮哄洗一体机',
          imgSrc: 'https://img.alicdn.com/imgextra/i3/32439009/O1CN01jI8kHo2GQB7Cn2FV5_!!0-saturn_solar.jpg_360x360xzq75.jpg_.webp',
          dan: 7999.00,
          num: 10
        },
      ],
      //热水器
      waterHeater: [
        {
          id: 13,
          name: '凯奇史密斯扁桶热水器',
          imgSrc: 'https://img.alicdn.com/imgextra/i1/4836973014/O1CN01hIRG1F1Y8Seidfhj6_!!0-saturn_solar.jpg_360x360xzq75.jpg_.webp',
          dan: 1699.00,
          num: 10
        }, {
          id: 14,
          name: '万家乐伺服恒温燃气热水器',
          imgSrc: 'https://img.alicdn.com/imgextra/i1/30191910/O1CN01mUhmbP1PypRkXqQQQ_!!0-saturn_solar.jpg_360x360xzq75.jpg_.webp',
          dan: 1699.00,
          num: 10
        },
      ],
      //生活电器
      homeAppliance: [
        {
          id: 15,
          name: '菜小厨双胆蒸箱电器',
          imgSrc: 'https://img.alicdn.com/imgextra/i2/2191090080/O1CN01mORM931CSge8mNHGV_!!0-saturn_solar.jpg_360x360xzq75.jpg_.webp',
          dan: 1599.00,
          num: 10
        },
        {
          id: 16,
          name: 'nesugar小巢手持挂烫机',
          imgSrc: 'https://img.alicdn.com/imgextra/i4/871390081/O1CN016YKha11CT92fQ65Bj_!!0-saturn_solar.jpg_360x360xzq75.jpg_.webp',
          dan: 298.00,
          num: 10
        },
      ],
    };
  },
  methods: {
    // 添加商品到购物车
    addg(item) {
      if (item.num > 0) {
        let product = this.shopping.find(p => p.id === item.id);
        if (product) {
          if (product.total < 10) { // 检查购物车中的商品数量是否小于10
            product.total++;
            item.num--;
          } else {
            alert('购物车中该商品数量已达最大库存');
          }
        } else {
          this.shopping.push({ ...item, total: 1, checked: false });
          item.num--;
        }
      } else {
        alert('库存不足');
      }
    },
    // 更新商品数量
    update(item, amount) {
      if (amount > 0) {
        let product = this.findProductById(item.id);
        if (product && product.num > 0) {
          if (item.total < 10) { // 检查购物车中的商品数量是否小于10
            item.total++;
            product.num--;
          } else {
            alert('购物车中该商品数量已达最大库存');
          }
        } else {
          alert('库存不足');
        }
      } else if (amount < 0 && item.total > 0) {
        item.total--;
        let product = this.findProductById(item.id);
        if (product) {
          product.num++;
        }
      }
    },
    // 删除商品
    del(index) {
      //删除商品时，将商品数量增加到库存中
      let item = this.shopping[index];
      //通过id找到商品，并将商品数量增加到库存中
      let product = this.findProductById(item.id);
      //如果商品存在，则将商品数量增加到库存中
      if (product) {
        product.num += item.total;
      }
      this.shopping.splice(index, 1);
    },
    // 查找商品
    findProductById(id) {
      switch (id) {
        case 1:
          return this.airConditioner;
        case 2:
          return this.tv;
        case 3:
          return this.fridge;
        case 4:
          return this.washingMachine;
        case 5:
          return this.waterHeater;
        case 6:
          return this.homeAppliance;
        default:
          return null;
      }
    },
    // tab 切换
    selectTab(tab) {
      this.selectedTab = tab;
    },
  },
  // 计算总价和计件
  computed: {
    // 计算总价
    getSum() {
      return this.shopping.reduce((sum, item) => {
        if (item.checked) {
          return sum + item.total * item.dan;
        } else {
          return sum;
        }
      }, 0).toFixed(2); // 保留两位小数
    },
    // 计算数量
    jSum() {
      return this.shopping.reduce((total, item) => {
        if (item.checked) {
          return total + item.total;
        } else {
          return total;
        }
      }, 0);
    },
    // 全选
    isCheckedAll: {
      get() {
        return this.shopping.every(item => item.checked);
      },
      set(value) {
        this.shopping.forEach(item => item.checked = value);
      }
    }
  }
};
</script>

<style lang="less">
.shop-list {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 30px;
}

.list-nav ul {
  display: flex;
  list-style: none;
  padding: 0;
  margin: 0;
}

.list-nav ul li {
  width: 100px;
  padding: 10px 20px;
  cursor: pointer;
  border: 1px solid #ddd;
  border-radius: 4px;
  background-color: #f9f9f9;
  transition: background-color 0.3s;
  text-align: center;
}

.list-nav ul li:hover {
  background-color: #dc5050;
}

.list-nav ul li.active {
  background-color: #dc5050;
  color: white;
}

.tab-content {
  margin-top: 20px;
  width: 100%;
  text-align: center;
}

.tab-content ul {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  grid-gap: 20px;
  list-style: none;

  p {
    font-size: 14px;
  }

  img {
    width: 250px;
    height: 250px;
  }

  li {
    border: 1px solid #ddd;
    border-radius: 4px;
    padding: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    transition: all 0.3s;
  }

  li:hover {
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
  }

  button {
    background-color: #dc5050;
    color: white;
    border: none;
    border-radius: 4px;
    padding: 10px 20px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
}

.shopping-cart {
  margin-top: 40px;

  table {
    width: 100%;
    border-collapse: collapse;
    border: 1px solid #ddd;
  }

  thead {
    background-color: #f9f9f9;
  }

  th,
  td {
    padding: 10px;
    text-align: center;
  }

  th {
    font-weight: bold;
  }

  tfoot {
    background-color: #f9f9f9;
    font-weight: bold;
  }

  button {
    background-color: #dc5050;
    color: white;
    border: none;
    border-radius: 4px;
    padding: 10px 20px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
}
</style>
