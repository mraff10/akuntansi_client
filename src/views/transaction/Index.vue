<template>
    <div class="container my-5">
        <div class="row justify-content-center">
            <div class="col-8">
                <router-link :to="{ name : 'transaction.create'}" class="btn btn-primary btn-sm rounded shadow mb-3">Add</router-link>
                
                <div class="card rounded shadow">
                    <div class="card-header">
                        Transaction List
                    </div>
                    <div class="card-body">
                        <table class="table">
                            <thead>
                                <tr>
                                    <th>Title</th>
                                    <th>Amount</th>
                                    <th>Type</th>
                                    <th>Action</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="(transaction, index) in transactions" :key="index">
                                    <td>{{ transaction.Judul }}</td>
                                    <td>{{ transaction.Jumlah_Pengeluaran }}</td>
                                    <td>{{ transaction.Jenis_Transaksi }}</td>
                                    <td>
                                        <div class="btn-group">
                                            <router-link :to="{ name: 'transaction.edit', params:{id: transaction.Slug}}" class="btn btn-sm btn-outline-info">Edit</router-link>
                                            <button class="btn btn-sm btn-outline-danger">
                                                Delete
                                            </button>
                                        </div>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios'


export default {
    data(){
return{
transactions: null
}
    },
    async mounted(){
    await axios.get('http://127.0.0.1:8000/api/transaction')
            .then((result) => {
                console.log(result.data.data)
                this.transactions = result.data.data
            }).catch((err) => {
                console.log(err.response)
            });
    },

}
</script>