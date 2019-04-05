<script>
import axios from "axios";

export default {
  name: "FetchData",
  props: {
    endpoint: {
      type: String,
      default: ""
    }
  },
  data() {
    return {
      data: null,
      pending: false,
      error: null
    };
  },
  watch: {
    endpoint: {
      immediate: true,
      handler: "fetchData"
    }
  },
  methods: {
    fetchData(endpoint) {
      console.log(endpoint);
      this.data = null;
      this.error = null;
      if (!endpoint.length) return;
      this.pending = true;
      axios
        .get(this.endpoint)
        .then(({ data }) => (this.data = data))
        .catch(error => (this.error = error))
        .finally(() => (this.pending = false));
    }
  },
  render() {
    return this.$scopedSlots.default({
      data: this.data,
      pending: this.pending,
      error: this.error
    });
  }
};
</script>
