<script>
	import { onMount } from 'svelte';
	import { BeButton } from '$lib';
  import BeTable from '$lib/be-table/BeTable.svelte';
  import BeTableColumn from '$lib/be-table/BeTableColumn.svelte';
  import {loading , loadingSerive} from '$lib'
  import DemoBlock from '$lib/demo/DemoBlock.svelte';
  const tableData = [{
        date: '2016-05-02',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
    }, {
        date: '2016-05-04',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1517 弄'
    }, {
        date: '2016-05-03',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1519 弄'
    }, {
        date: '2016-05-01',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1519 弄'
    }];
  let load = true
  onMount(()=> {
    // setTimeout(() => {
    //   load = true
    //   setTimeout(() => {
    //     load = false
    //   }, 5000);
    // }, 5000);
  })
  // 服务方式
  function showLoading() {
    let loadingInstance1 = new loadingSerive({
      target: '.test2',
      text:'loading',
      // background: 'rgba(0, 0, 0, 0.8)'
    })
    loadingInstance1.show()
    // setTimeout(() => {
    //   loadingInstance1.close()
    //   }, 5000);
  }
  </script>



<div class='page-container'>
  <h2>Loading 加载</h2>
  <p>加载数据时显示动效。</p>
  <h3>区域加载</h3>
  <p>在表格等容器中加载数据时显示。</p>
  <!-- 标签指令的方式 -->
  <DemoBlock code={`
    <div use:loading={load}>
      <BeTable data={tableData}>
        <BeTableColumn prop="name" label="姓名" />
        <BeTableColumn prop="date" label="日期" />
        <BeTableColumn prop="address" label="地址" />
      </BeTable>
    </div>`}
    js={`
    import { BeTable, BeTableColumn } from '@brewer/beerui'
    import {loading} from '$lib/utils/loading'
    const load = true
    const tableData = [{
      date: '2016-05-02',
      name: '王小虎',
      address: '上海市普陀区金沙江路 1518 弄'
    }, {
      date: '2016-05-04',
      name: '王小虎',
      address: '上海市普陀区金沙江路 1517 弄'
    }, {
      date: '2016-05-03',
      name: '王小虎',
      address: '上海市普陀区金沙江路 1519 弄'
    }, {
      date: '2016-05-01',
      name: '王小虎',
      address: '上海市普陀区金沙江路 1519 弄'
    }]`
    }
        >
      <div slot='source'>
          <!-- <h3>标签指令Loading</h3> -->
          <div use:loading={load}>
            <BeTable data={tableData}>
              <BeTableColumn prop="name" label="姓名" />
              <BeTableColumn prop="date" label="日期" />
              <BeTableColumn prop="address" label="地址" />
            </BeTable>
        </div>
      </div>
      <div slot='description'>
        BeerUi 提供了两种调用 Loading 的方法：指令和服务。对于指令标签use:loading，只需要绑定Boolean即可。默认状况下，Loading 遮罩会插入到绑定元素的子节点。
      </div>
  </DemoBlock>

  <!-- <div class="test" use:loading={load} loading-text="拼命加载中" loading-background='rgba(0, 0, 0, 0.8)' style="height:300px;" >111111111111111111111111111111111111111111111111</div> -->

  <!-- <div class="test2" style="height:300px;" >1111111111</div> -->

  <BeButton class='demo-button' size="normal" type="primary" on:click={showLoading}>默认按钮</BeButton>
</div>
