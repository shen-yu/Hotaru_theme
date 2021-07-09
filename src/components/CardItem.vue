<template>
  <div class="column">
    <div class="ui fluid card">
      <div class="card-header">
        <svg viewBox="0 0 100 100" class="flag-icon">
          <use :xlink:href="`#${server.region}`"></use>
        </svg>
        <span> {{ server.name }} 【{{ server.location }}】 </span>
        <p>{{ server.type }}</p>
      </div>
      <div class="ui tiny progress success">
        <div
          class="bar"
          :style="{ width: getStatus ? `${getRAMStatus.toString()}%` : '0%' }"
        ></div>
      </div>
      <div class="card-content">
        <p>
          实时网络：{{
            `↓ ${tableRowByteConvert(
              server.network_rx
            )} | ↑ ${tableRowByteConvert(server.network_tx)}`
          }}
        </p>
        <p>
          流量合计：{{
            `↓ ${tableRowByteConvert(
              server.network_in
            )} | ↑ ${tableRowByteConvert(server.network_out)}`
          }}
        </p>
        <p>
          内存信息：{{
            `${expandRowByteConvert(
              server.memory_used * 1024
            )} / ${expandRowByteConvert(server.memory_total * 1024)}`
          }}
        </p>
        <p>
          硬盘信息：{{
            `${expandRowByteConvert(
              server.hdd_used * 1024 * 1024
            )} / ${expandRowByteConvert(server.hdd_total * 1024 * 1024)}`
          }}
        </p>
        <p>
          CPU使用率：{{ `${getCpuStatus.toString()}%` }} ❤ 已开机：{{
            server.uptime
          }}
        </p>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';
import useStatus from './useStatus';

export default defineComponent({
  name: 'CardItem',
  props: {
    server: {
      type: Object as PropType<StatusItem | BoxItem>,
      default: () => ({})
    }
  },
  setup(props) {
    const {
      getStatus,
      getRAMStatus,
      tableRowByteConvert,
      expandRowByteConvert,
      getCpuStatus
    } = useStatus(props);
    return {
      getStatus,
      getRAMStatus,
      tableRowByteConvert,
      expandRowByteConvert,
      getCpuStatus
    };
  }
});
</script>

<style scoped>
div.card {
  padding: 24px;
  box-shadow: 5px 5px 25px 0 rgba(46, 61, 73, 0.2);
  border-radius: 0.5rem;
  background-color: rgba(255, 255, 255, 0.8);
}

div.card div.card-header span {
  font-size: 1.25rem;
  font-weight: normal;
  vertical-align: middle;
}

div.card div.card-header p {
  color: #919699;
}

div.card div.card-content p {
  margin-bottom: 0;
}

div.card div.progress {
  margin: 1.2em 0;
}

.flag-icon {
  display: inline;
  vertical-align: middle;
  width: 70px;
  margin-right: 8px;
}
</style>
