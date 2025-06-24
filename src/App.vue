<template>
  <div class="h-screen flex flex-col items-center justify-center gap-4 bg-gray-100 px-4">
    <input
      v-model="note"
      placeholder="Nhập ghi chú..."
      class="w-full max-w-md px-4 py-2 border rounded-xl shadow"
    />
    <button
      @click="sendTimestamp"
      class="bg-blue-600 text-white px-10 py-4 rounded-xl text-lg shadow-lg hover:bg-blue-700"
    >
      Ghi thời gian
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      note: "",
    };
  },
  methods: {
    async sendTimestamp() {
      try {
        const params = new URLSearchParams({ note: this.note });
        await fetch("https://script.google.com/macros/s/AKfycbwcsGOnnGw0OxD8GincWuT7MOzgkKSpJlSTerKKTe_AhJ1IfybCn1kFZGYWv3DOKS5q/exec?" + params.toString(), {
          method: "POST",
        });
        alert("✅ Đã gửi!");
        this.note = ""; // reset ô nhập
      } catch (err) {
        alert("❌ Lỗi khi gửi.");
        console.error(err);
      }
    },
  },
};
</script>
