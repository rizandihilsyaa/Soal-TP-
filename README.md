#include <stdio.h>
#include <stdlib.h>

typedef struct {
    int id;
    int threat;
    float speed;
} Object;

int main() {
    int N;
    printf("Masukkan jumlah puing objek: ");
    scanf("%d", &N);
    
    Object *objects = malloc(N * sizeof(Object));
    printf("Masukkan ID, Ancaman (0-100), Kecepatan untuk setiap objek:\n");
    for(int i = 0; i < N; i++) {
        scanf("%d %d %f", &objects[i].id, &objects[i].threat, &objects[i].speed);
    }
    
    // Hapus duplikat berdasarkan ID
    Object *unique = malloc(N * sizeof(Object));
    int unique_count = 0;
    for(int i = 0; i < N; i++) {
        int duplicate = 0;
        for(int j = 0; j < unique_count; j++) {
            if(unique[j].id == objects[i].id) {
                duplicate = 1;
                break;
            }
        }
        if(!duplicate) {
            unique[unique_count++] = objects[i];
        }
    }
    
    // Bubble Sort: Ancaman descending, jika sama maka Kecepatan ascending
    for(int i = 0; i < unique_count - 1; i++) {
        for(int j = 0; j < unique_count - 1 - i; j++) {
            if((unique[j].threat < unique[j+1].threat) ||
               (unique[j].threat == unique[j+1].threat && unique[j].speed > unique[j+1].speed)) {
                Object temp = unique[j];
                unique[j] = unique[j+1];
                unique[j+1] = temp;
            }
        }
    }
    
    // Output
    printf("Puing objek yang Diurutkan (Ancaman Tertinggi Dahulu):\n");
    printf("ID:");
    for(int i = 0; i < unique_count; i++) {
        printf(" %d", unique[i].id);
    }
    printf("\nAncaman:");
    for(int i = 0; i < unique_count; i++) {
        printf(" %d", unique[i].threat);
    }
    printf("\nKecepatan:");
    for(int i = 0; i < unique_count; i++) {
        printf(" %.0f", unique[i].speed);
    }
    printf("\n");
    
    free(objects);
    free(unique);
    return 0;
}
