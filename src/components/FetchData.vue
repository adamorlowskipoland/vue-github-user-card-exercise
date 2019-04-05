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
  created() {
    console.log(this.endpoint);
    this.data = null;
    this.error = null;
    if (!this.endpoint.length) return;
    this.pending = true;
    axios
      .get(this.endpoint)
      .then(({ data }) => (this.data = data))
      .catch(error => (this.error = error))
      .finally(() => (this.pending = false));
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
